---
type: srs-flows
feature: sport-matching
updated: 2026-06-04
---

# Sport Matching — Sequence & Activity Diagrams

## Flow: Registration + OTP

- **Trigger:** Player mở app lần đầu, chọn Đăng ký
- **Related UC:** uc-register
- **Related FR:** FR-sport-matching-001, FR-sport-matching-002

```mermaid
sequenceDiagram
    actor P as Player
    participant App as Mobile App
    participant BE as Backend
    participant Email as Email Service

    P->>App: Nhập email + mật khẩu + tên hiển thị
    App->>BE: POST /register
    BE->>BE: Validate email format + unique
    alt Email đã tồn tại
        BE-->>App: Error: email đã đăng ký
        App-->>P: Hiện thông báo lỗi
    else Email hợp lệ
        BE->>BE: Tạo account (status: unverified)
        BE->>Email: Gửi OTP 6 số (expire 5 phút)
        Email-->>P: Email chứa OTP
        BE-->>App: OK, chờ OTP
        App-->>P: Hiện màn hình nhập OTP
        P->>App: Nhập OTP
        App->>BE: POST /verify-otp
        alt OTP đúng + chưa hết hạn
            BE->>BE: Account verified
            BE-->>App: OK, chuyển setup profile
            App-->>P: Hiện màn profile-setup
            P->>App: Chọn môn + trình độ per môn
            App->>BE: POST /profile/sports
            BE-->>App: Profile hoàn tất
            App-->>P: Hiện màn map-search (main)
        else OTP sai hoặc hết hạn
            BE-->>App: Error: OTP invalid
            App-->>P: Hiện lỗi, option Gửi lại
        end
    end
```

## Flow: Matching + Booking + Invite

- **Trigger:** Player mở app, chọn môn, tìm đối thủ
- **Related UC:** uc-find-opponent, uc-book-match
- **Related FR:** FR-sport-matching-003 đến FR-sport-matching-010

```mermaid
sequenceDiagram
    actor P1 as Player
    participant App as Mobile App
    participant BE as Backend
    participant Map as Map API
    participant FCM as FCM
    actor P2 as Opponent

    P1->>App: Mở app
    App->>BE: GET /location (GPS auto)
    alt GPS OFF
        BE-->>App: E-sport-matching-001
        App-->>P1: Thông báo bật GPS
    else GPS OK
        BE->>Map: Reverse geocode vị trí
        Map-->>BE: Location data
        BE-->>App: Vị trí xác định
        App-->>P1: Hiện bản đồ + vị trí

        P1->>App: Chọn môn + filter (bán kính, trình độ)
        App->>BE: GET /opponents?sport=X&radius=3km&level=Y
        BE->>BE: Tính Matching Score per opponent
        
        alt Không có đối thủ
            BE-->>App: E-sport-matching-006
            App-->>P1: Gợi ý mở rộng filter
        else Có đối thủ
            BE-->>App: Danh sách opponents sorted by Score
            App-->>P1: Hiện opponents trên bản đồ

            P1->>App: Chọn đối thủ
            App-->>P1: Hiện opponent-profile

            P1->>App: Chọn sân + slot giờ
            App->>BE: POST /slots/{id}/lock
            
            alt Slot đã bị lock
                BE-->>App: E-sport-matching-007
                App-->>P1: Gợi ý slot/sân khác
            else Slot trống
                BE->>BE: Lock slot 5 phút (Pessimistic)
                Note over BE: Timer 5 phút bắt đầu

                alt Đã có match pending
                    BE-->>App: E-sport-matching-004
                    App-->>P1: Yêu cầu hủy match cũ
                else Không có pending
                    alt Vượt 10 invite/ngày/môn
                        BE-->>App: E-sport-matching-005
                        App-->>P1: Gợi ý Premium
                    else Còn quota
                        BE->>BE: Tạo Match + Invite (pending)
                        BE->>FCM: Push notification cho P2
                        FCM-->>P2: Thông báo invite
                        BE-->>App: Invite sent, đang chờ
                        App-->>P1: Hiện countdown 5 phút

                        alt P2 Accept trong 5 phút
                            P2->>BE: POST /invites/{id}/accept
                            BE->>BE: Match confirmed
                            BE->>FCM: Notify cả 2
                            FCM-->>P1: Match confirmed!
                            FCM-->>P2: Match confirmed!
                        else P2 Reject
                            P2->>BE: POST /invites/{id}/reject
                            BE->>BE: Release slot
                            BE->>FCM: Notify P1
                            FCM-->>P1: E-sport-matching-003
                        else Timeout 5 phút
                            BE->>BE: Auto hủy invite + release slot
                            BE->>BE: Tìm đối thủ tiếp (next Score)
                            BE->>FCM: Notify P1
                            FCM-->>P1: E-sport-matching-002
                        end
                    end
                end
            end
        end
    end
```

## Flow: Rating + Auto-adjust

- **Trigger:** Trận đấu hoàn thành, system gửi nhắc nhở
- **Related UC:** uc-rate-opponent
- **Related FR:** FR-sport-matching-011, FR-sport-matching-014

```mermaid
sequenceDiagram
    actor P as Player
    participant App as Mobile App
    participant BE as Backend
    participant FCM as FCM

    Note over BE: Trận đấu status: Hoàn thành
    BE->>FCM: Nhắc nhở đánh giá
    FCM-->>P: Push notification
    P->>App: Mở đánh giá
    App-->>P: Hiện màn rate-opponent
    P->>App: Chấm rating (1-5) + nhận xét
    App->>BE: POST /ratings
    BE->>BE: Cập nhật rating_avg đối thủ
    BE->>BE: Check ELO auto-adjust
    alt Rating liên tục cao hơn bậc hiện tại
        BE->>BE: Tăng skill_level đối thủ
        BE->>BE: Cập nhật Matching Score
        BE->>FCM: Notify đối thủ về rank up
    else Rating bình thường
        Note over BE: Giữ nguyên skill_level
    end
    BE-->>App: Đánh giá gửi thành công
    App-->>P: Xác nhận + quay về match-history
```
