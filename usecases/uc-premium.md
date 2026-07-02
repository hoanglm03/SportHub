# UC: Mua Premium Subscription (uc-premium)

## a. Mục đích

Player free mua gói Premium 49.000 VND/tháng để unlock unlimited invite mỗi ngày (bỏ giới hạn 10 invite/ngày/môn). System gợi ý upgrade khi Player đạt limit.

## b. Actors

- **Player (Free)** — người mua gói
- **System** — xử lý subscription, activate quyền lợi, gia hạn/hết hạn
- **Payment Gateway** (MoMo/VNPay) — thanh toán recurring

## c. Pre-conditions

- Player đã đăng nhập (role: Player, tier: Free)
- CAP-12 (P1) đã active
- CAP-08 (Thanh toán online) đã active

## d. Expected result

**Luồng mua Premium từ gợi ý:**
1. Player gửi invite thứ 11 trong ngày → E-sport-matching-005 xuất hiện kèm nút "Nâng cấp Premium"
2. Player tap → màn `premium-upgrade`, xem quyền lợi + giá 49.000đ/tháng
3. Player chọn thanh toán (MoMo/VNPay), hoàn tất
4. Account chuyển sang Premium, badge Premium hiện trên profile, invite limit removed ngay lập tức

**Luồng mua Premium chủ động:**
1. Player vào Settings → "Nâng cấp Premium"
2. Xem màn `premium-upgrade`, mua, kết quả như trên

**Luồng hết hạn:**
1. Cuối chu kỳ tháng, nếu không gia hạn → account quay về Free
2. Player nhận notification "Gói Premium đã hết hạn, invite giới hạn 10/ngày/môn"
3. Invite đang pending không bị hủy, chỉ giới hạn áp dụng từ ngày tiếp theo

## e. Activity diagram

Không bắt buộc.

## f. Screens involved

- `premium-upgrade` — trang giới thiệu gói + mua
- `settings` — entry point truy cập Premium từ menu
- `map-search` — gợi ý khi đạt limit (E-005 banner)

## g. FR map

| FR | Mô tả |
|----|-------|
| FR-sport-matching-017 | Premium 49k/tháng, unlimited invite, gợi ý khi đạt limit |

## h. Open Questions

Không có OQ mở.
