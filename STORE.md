# WOLMASTER – Hồ sơ phát hành App Store & Google Play

Tài liệu này gồm: (1) những việc **bạn phải tự làm** vì cần tài khoản, máy hoặc chữ ký của bạn, (2) nội dung điền sẵn cho
hai store, (3) câu trả lời cho các bảng khai báo. Phần mã nguồn đã được chuẩn bị xong – xem mục cuối.

> Yêu cầu của store thay đổi hằng năm. Các con số dưới đây đúng tại thời điểm viết (11/2026); hãy đối chiếu trang chính thức
> trước khi nộp: [Google Play target API](https://support.google.com/googleplay/android-developer/answer/11926878),
> [Apple upcoming requirements](https://developer.apple.com/news/upcoming-requirements/).

---

## 0. Những việc phải quyết định trước tiên

| Việc | Vì sao phải làm trước | Sửa ở đâu |
| --- | --- | --- |
| **Đổi `appId`** từ `com.wolmaster.app` sang tên miền đảo ngược bạn sở hữu (ví dụ `vn.tencongty.wolmaster`) | Đây là định danh vĩnh viễn trên cả hai store, **không đổi được sau lần phát hành đầu** | `capacitor.config.ts`, rồi xoá hai thư mục `android/` và `ios/`, chạy lại `npx cap add android && npx cap add ios && npm run assets`, sau đó áp lại các chỉnh ở mục 5 |
| ~~Điền tên nhà phát triển, email liên hệ và luật áp dụng~~ – **đã xong** (18/11/2026) | Cả hai store bắt buộc chính sách nêu rõ ai phát hành và cách liên hệ | Nguyễn Đình Thắng (Nguyen Dinh Thang) · nthang621@gmail.com · luật Việt Nam, trong `public/privacy.html`, `support.html`, `terms.html` |
| **Đăng 3 trang lên một địa chỉ web công khai** (HTTPS, không cần đăng nhập) | Hai store chỉ nhận URL, không nhận tệp; Google sẽ từ chối nếu link hỏng hoặc trả về PDF | Xem mục 2b |
| **Tra nhãn hiệu "WOLMASTER"** | Tên trùng nhãn hiệu đã đăng ký có thể bị gỡ khỏi store | Tra trên cơ sở dữ liệu nhãn hiệu của Cục SHTT và trên chính hai store |

---

## 1. Việc bạn cần làm – Google Play

1. Tạo tài khoản [Google Play Console](https://play.google.com/console) (phí một lần).
   Tài khoản **cá nhân** tạo sau 13/11/2023 phải chạy *thử nghiệm kín* với **ít nhất 12 người, liên tục 14 ngày** trước khi xin
   phát hành chính thức. Tài khoản tổ chức không cần nhưng phải có mã D‑U‑N‑S.
2. Cài [Android Studio](https://developer.android.com/studio) (kèm Android SDK 36 và JDK).
3. Trong thư mục dự án:
   ```bash
   npm run android
   ```
   Lệnh này build bản web, đồng bộ sang `android/` và mở Android Studio.
4. Chạy thử trên **máy Android thật** (xem danh sách kiểm tra ở mục 4).
5. Tạo khoá ký: *Build → Generate Signed App Bundle → Create new keystore*. **Giữ kỹ tệp keystore và mật khẩu** – mất là không
   cập nhật được ứng dụng. Bật *Play App Signing* khi tải lên.
6. Xuất tệp `.aab` (Android App Bundle) và tải lên track *Closed testing*.
7. Điền hồ sơ theo mục 2 và 3, mời 12 người thử, chờ đủ 14 ngày rồi bấm *Apply for production*.

## 1b. Việc bạn cần làm – App Store

1. Đăng ký [Apple Developer Program](https://developer.apple.com/programs/) (phí hằng năm).
2. Cài **Xcode 26 trở lên** từ Mac App Store (máy này hiện chỉ có Command Line Tools), mở một lần để cài iOS SDK.
3. Trong thư mục dự án:
   ```bash
   npm run ios
   ```
4. Trong Xcode: chọn target **App → Signing & Capabilities**, chọn Team của bạn (Xcode tự tạo chứng chỉ và provisioning).
5. Chạy thử trên **iPhone thật** (mục 4).
6. *Product → Archive → Distribute App → App Store Connect*.
7. Trên [App Store Connect](https://appstoreconnect.apple.com): tạo ứng dụng với đúng bundle id, điền hồ sơ (mục 2, 3),
   dán "Ghi chú cho người duyệt" (mục 3.4), gửi duyệt. Nên phát qua TestFlight cho vài người trước.

---

## 2. Nội dung hồ sơ (điền sẵn)

### Tên & mô tả ngắn

| Trường | Giới hạn | Tiếng Việt | English |
| --- | --- | --- | --- |
| Tên ứng dụng | 30 ký tự | WOLMASTER: Quản trò Ma Sói | WOLMASTER: Werewolf Moderator |
| Phụ đề (App Store) | 30 ký tự | Điều hành Ma Sói ngoài đời | Run real-life Werewolf nights |
| Mô tả ngắn (Play) | 80 ký tự | Trợ lý quản trò Ma Sói: setup nhanh, gọi đêm từng bước, không cần mạng. | Werewolf moderator's helper: fast setup, guided nights, fully offline. |
| Từ khoá (App Store) | 100 ký tự | ma sói,quản trò,werewolf,mafia,boardgame,party,trò chơi nhóm,phân vai,đếm phiếu | werewolf,mafia,moderator,game master,party game,narrator,roles,voting,timer |

### Mô tả đầy đủ – Tiếng Việt

```
WOLMASTER là trợ lý dành cho QUẢN TRÒ khi chơi Ma Sói bằng bài thật ngoài đời. Người chơi không cần cài gì – chỉ quản trò
cầm máy để không quên lượt, không nhầm vai và không phải ghi chép.

SETUP TRONG MỘT PHÚT
• Dán danh sách tên hoặc nhập số người (tối đa 50), ghế được tạo tự động
• Gợi ý bộ vai trò theo số người, chỉnh bằng + / −
• Phát bài thật xong thì chạm vào từng ghế để chọn lá bài bằng hình minh hoạ
• Ván sau giữ nguyên danh sách người chơi, không phải nhập lại

ĐIỀU HÀNH ĐÊM TỪNG BƯỚC
• Ứng dụng nhắc đúng thứ tự gọi và lời gọi cho từng vai
• Chỉ cho chọn mục tiêu hợp lệ; tự tính bảo vệ, cứu, độc, cặp đôi chết theo nhau
• Bạn xem lại và xác nhận kết quả trước khi trời sáng; nhầm thì hoàn tác

BAN NGÀY & BỎ PHIẾU
• Đồng hồ thảo luận lớn, cộng trừ thời gian nhanh
• Đếm giơ tay hoặc ghi từng phiếu; xử lý hoà phiếu và bỏ phiếu lại

21 VAI TRÒ CÓ SẴN, THÊM ĐƯỢC VAI RIÊNG
Dân làng, Tiên tri, Bảo vệ, Phù thủy, Thợ săn, Cupid, Già làng, Thị trưởng, Hoàng tử, Người bị nguyền, Người lai sói,
Thầy bùa, Hội kín, Sói, Sói ẩn mình, Sói tiên tri, Sói điên, Tay sai, Kẻ ngốc, Sát nhân, Kẻ thổi sáo.
Luật chơi tuỳ chỉnh được theo cách bàn của bạn vẫn chơi.

GIỮ BÍ MẬT
• Một chạm để che toàn bộ màn hình, phải giữ nút mới mở lại
• Tự che khi bạn khoá máy hoặc chuyển ứng dụng

AN TOÀN DỮ LIỆU
• Tự lưu sau mỗi thao tác – tắt máy mở lại vẫn đúng bước đang gọi
• Hoạt động hoàn toàn không cần mạng
• Không tài khoản, không quảng cáo, không thu thập dữ liệu
```

### Full description – English

```
WOLMASTER is a helper for the MODERATOR of a real-life Werewolf (Mafia) game played with physical cards. Players install
nothing – only the moderator holds the phone, so no turn is forgotten, no role is mixed up and nothing needs writing down.

SET UP IN A MINUTE
• Paste a list of names or pick a player count (up to 50); seats are created for you
• Role sets suggested for your player count, adjustable with + / −
• After dealing the real cards, tap each seat and pick its card by picture
• The next game keeps the same players – no retyping

GUIDED NIGHTS
• The app prompts the right calling order and the line to say for every role
• Only valid targets can be picked; protection, healing, poison and lovers are resolved for you
• Review and confirm the outcome before dawn; undo if you slip

DAY AND VOTING
• Large discussion timer with quick add/subtract
• Count raised hands or record each ballot; ties and revotes are handled

21 BUILT-IN ROLES, PLUS YOUR OWN
Villager, Seer, Guardian, Witch, Hunter, Cupid, Elder, Mayor, Prince, Cursed, Lycan, Silencer, Masons, Werewolf, Hidden
Wolf, Wolf Seer, Rabid Wolf, Minion, Jester, Killer, Piper. Rules can be tuned to match how your table plays.

KEEP SECRETS SECRET
• One tap covers the whole screen; press and hold to reveal
• Covers itself when you lock the phone or switch apps

YOUR DATA STAYS YOURS
• Saves after every action – reopen the app and you are on the exact same step
• Works fully offline
• No account, no ads, no data collection
```

> Giao diện ứng dụng có **8 ngôn ngữ** (Việt, Anh Mỹ, Anh Anh, Pháp, Nga, Trung giản thể, Hàn, Nhật) và tự chọn theo ngôn ngữ thiết bị.
> Hồ sơ store ở trên mới viết sẵn tiếng Việt và tiếng Anh; nếu phát hành ở thị trường khác, nên thêm mô tả cùng ngôn ngữ đó trong
> Play Console / App Store Connect (mỗi ngôn ngữ một bản mô tả và bộ ảnh chụp màn hình riêng).

### Thông tin khác

| Trường | Giá trị đề xuất |
| --- | --- |
| Danh mục – Google Play | Ứng dụng → **Công cụ** (hoặc Giải trí) |
| Danh mục – App Store | **Utilities** (phụ: Entertainment) |
| Giá | Miễn phí, không mua trong ứng dụng |
| URL chính sách quyền riêng tư / hỗ trợ / điều khoản | Xem mục 2b |
| Phiên bản | 1.0.0 (versionCode / build 1) |
| Thiết bị | Điện thoại, màn hình dọc. iOS: chỉ iPhone (iPad chạy ở chế độ tương thích) |

### 2b. Trang công khai bắt buộc

| Trang | Tệp | App Store | Google Play | Trong ứng dụng |
| --- | --- | --- | --- | --- |
| Chính sách quyền riêng tư | `public/privacy.html` | **Bắt buộc** – ô *Privacy Policy URL* (App Information) | **Bắt buộc** – *App content → Privacy policy* và mục *Store listing* | *Cài đặt → Chính sách quyền riêng tư* |
| Hỗ trợ (liên hệ + FAQ) | `public/support.html` | **Bắt buộc** – ô *Support URL* của mỗi phiên bản | Không bắt buộc (bắt buộc có **email liên hệ** ở *Store settings*); có thể điền vào ô *Website* | *Cài đặt → Trợ giúp & hỗ trợ* |
| Điều khoản sử dụng | `public/terms.html` | Không bắt buộc – nếu để trống, Apple dùng EULA chuẩn. Có thể dán link vào cuối mô tả | Không bắt buộc | *Cài đặt → Điều khoản sử dụng* |
| Marketing URL | – | Không bắt buộc | – | – |

Cả ba trang song ngữ Việt/Anh, dùng chung `public/legal.css`, liên kết qua lại và được build vào `dist/` cùng ứng dụng
(nên mở được cả khi offline). Cách đăng nhanh nhất là đưa nguyên thư mục `dist/` lên một dịch vụ host tĩnh miễn phí:

- **GitHub Pages**: tạo repo, đẩy nội dung `dist/` lên nhánh `gh-pages` → `https://<tên>.github.io/<repo>/privacy.html`.
- **Netlify / Cloudflare Pages**: kéo thả thư mục `dist/` → nhận ngay một địa chỉ `https://…`.

**Chỉ đăng 3 trang lên GitHub Pages (đề xuất):** chạy `npm run pages` để gom sẵn vào `store/pages/`, rồi:

1. Trên github.com bấm **New repository**, đặt tên `wolmaster`, chọn **Public**, tick *Add a README file*, bấm *Create*.
2. Trong repo: **Add file → Upload files**, kéo toàn bộ tệp trong `store/pages/` vào, bấm *Commit changes*.
3. **Settings → Pages**: *Source* = *Deploy from a branch*, *Branch* = `main`, thư mục `/ (root)`, bấm *Save*.
4. Chờ 1–2 phút, link sẽ là `https://<tên-tài-khoản>.github.io/wolmaster/privacy.html` (tương tự `support.html`, `terms.html`).

Khi sửa nội dung trang: sửa trong `public/`, chạy lại `npm run pages`, tải lại tệp đã đổi lên repo (ghi đè).

Nếu muốn đăng cả bản web của ứng dụng thì đưa nguyên `dist/` lên thay vì `store/pages/`. 
Sau khi đăng, mở thử trên điện thoại cả ba link (không đăng nhập, không chuyển hướng lạ) rồi mới dán vào hai store. Khi sửa nội
dung, đổi ngày *Có hiệu lực từ / Effective* ở đầu trang.

### Hình ảnh

| Hình | Trạng thái |
| --- | --- |
| Icon Play 512×512 | ✅ `store/graphics/play-icon-512.png` |
| Ảnh bìa Play 1024×500 | ✅ `store/graphics/play-feature-graphic-1024x500.png` |
| Icon App Store 1024×1024 | ✅ `store/graphics/appstore-icon-1024.png` (đã nằm sẵn trong dự án Xcode) |
| Ảnh chụp màn hình | ⬜ **Bạn cần chụp trên máy thật / máy ảo.** Play: tối thiểu 2 ảnh điện thoại. App Store: bộ ảnh iPhone 6,9 inch. Gợi ý 5 màn: chọn vai bằng hình, bước gọi Sói, tổng hợp đêm, đồng hồ thảo luận, kết quả bỏ phiếu |

---

## 3. Câu trả lời cho các bảng khai báo

### 3.1 Google Play – Data safety

| Câu hỏi | Trả lời |
| --- | --- |
| Ứng dụng có thu thập hoặc chia sẻ dữ liệu người dùng không? | **Không** |
| Dữ liệu có được mã hoá khi truyền không? | Không áp dụng (không truyền dữ liệu) |
| Người dùng có thể yêu cầu xoá dữ liệu không? | Không áp dụng; dữ liệu chỉ ở trên máy và xoá được trong ứng dụng |

Các mục khác: *Ads* – Không. *App access* – Toàn bộ chức năng dùng được, không cần đăng nhập. *Target audience* – 13 tuổi trở lên.
*News app*, *COVID‑19*, *Government*, *Financial*, *Health* – Không.

### 3.2 App Store – App Privacy

Chọn **"Data Not Collected"**. Ứng dụng không dùng API theo dõi nên không cần App Tracking Transparency.
*Export compliance*: ứng dụng không dùng mã hoá (đã khai sẵn `ITSAppUsesNonExemptEncryption = false` trong `Info.plist`).

### 3.3 Phân loại độ tuổi

Nội dung chỉ là chữ và hình minh hoạ, nhắc tới việc nhân vật trong trò chơi bị "cắn", "giết", "treo cổ".

| Câu hỏi | Trả lời |
| --- | --- |
| Bạo lực hoạt hình / giả tưởng | **Nhẹ, không thường xuyên** (chỉ nhắc bằng chữ) |
| Bạo lực chân thực, máu me, kinh dị | Không |
| Nội dung tình dục, chất kích thích, cờ bạc, ngôn từ tục | Không |
| Nội dung do người dùng tạo / chat / mạng xã hội | Không (tên người chơi chỉ lưu trên máy, không chia sẻ) |
| Truy cập web không giới hạn | Không |

### 3.4 Ghi chú cho người duyệt (App Store – "Notes for Review")

```
WOLMASTER is a companion tool for the moderator of an in-person Werewolf/Mafia card game. It is not a website wrapper:
all content and logic are bundled in the app and it works with no network connection (please try it in Airplane Mode).

No account or login is needed. The app follows the device language (English, French, Russian, Simplified Chinese,
Korean, Japanese or Vietnamese) and can be changed in Settings → Language. To try it quickly (English labels):
1. Tap "New game" → tab "Count" → "8 players" → "Continue" twice.
2. On the last step choose "Random" → "START GAME".
3. Follow the guided night steps with the gold "Next step" / "Confirm" button at the bottom.

Native capabilities used: haptic feedback, keeping the screen awake during a game, the system share sheet to export
backups and results, and native storage so an in-progress game survives the app being closed.
The app collects no data.
```

---

## 4. Danh sách kiểm tra trên máy thật (chưa ai làm)

Bản đóng gói **chưa từng được build hay chạy trên thiết bị** – máy phát triển không có Xcode và Android SDK. Trước khi nộp, hãy
kiểm tra trên một iPhone và một máy Android:

- [ ] Ứng dụng mở được, màn hình chờ và icon hiển thị đúng
- [ ] Nội dung không bị tai thỏ / thanh điều hướng che (đầu và cuối màn hình)
- [ ] Chạy trọn một ván ở **chế độ máy bay**
- [ ] Giữa đêm: vuốt tắt hẳn ứng dụng rồi mở lại → đúng bước đang gọi
- [ ] *Sao lưu & khôi phục → Xuất tệp*: bảng chia sẻ mở ra, lưu được tệp; sau đó nhập lại được tệp đó
- [ ] *Xuất kết quả* ở màn kết thúc ván mở bảng chia sẻ
- [ ] Rung khi thao tác; màn hình không tự tắt trong ván
- [ ] Nút "Dán từ bộ nhớ tạm" đọc được danh sách tên
- [ ] Android: nút Back đóng sheet → lùi bước → lùi màn → thu nhỏ ứng dụng ở trang chủ; không thoát mất ván
- [ ] Nút che màn hình; khoá máy rồi mở lại thấy màn hình trung tính
- [ ] Chữ không bị vỡ khi bật cỡ chữ hệ thống lớn
- [ ] 30–50 người chơi: cuộn mượt, lưới chọn mục tiêu bấm chính xác

---

## 5. Phần đã chuẩn bị trong mã nguồn

| Hạng mục | Chi tiết |
| --- | --- |
| Vỏ native | Capacitor 8; dự án `android/` (target & compile SDK 36, min SDK 24) và `ios/` (iOS 15+, Swift Package Manager) |
| Cấu hình | `capacitor.config.ts`; khoá màn hình dọc; iOS chỉ iPhone; phiên bản 1.0.0 |
| Icon & màn hình chờ | Sinh từ một nguồn vẽ duy nhất bằng `npm run assets` (74 tệp Android, 7 tệp iOS, icon PWA, hình cho store) |
| Lưu trữ | Ván đang chơi, thư viện, cài đặt, bản nháp thiết lập được ghi thêm vào kho native và tự khôi phục nếu WebView bị dọn dữ liệu |
| Xuất tệp | Ghi tệp tạm rồi mở bảng chia sẻ của hệ điều hành (thay cho tải xuống kiểu trình duyệt) |
| Rung, giữ màn hình sáng | Dùng plugin native; trên web vẫn dùng API trình duyệt |
| Nút Back Android | Đóng sheet → màn hình tự xử lý → lùi lịch sử → thu nhỏ ứng dụng |
| Trang công khai | `public/privacy.html`, `support.html`, `terms.html` (Việt + Anh), mở được trong *Cài đặt* (bản tiếng Việt khi giao diện tiếng Việt, bản English với các ngôn ngữ khác) |
| Quyền hệ thống | Android: `INTERNET` (WebView nội bộ cần) và `VIBRATE` (plugin rung tự thêm) – cả hai đều không hiện hộp thoại xin quyền; iOS không xin quyền nào |

Các chỉnh tay trong dự án native (cần áp lại nếu tạo lại `android/` hoặc `ios/`):

- `android/app/src/main/AndroidManifest.xml`: `android:screenOrientation="portrait"` ở `MainActivity`
- `android/app/build.gradle`: `versionName "1.0.0"`
- `ios/App/App/Info.plist`: chỉ còn `UIInterfaceOrientationPortrait`; thêm `ITSAppUsesNonExemptEncryption = false`
- `ios/App/App.xcodeproj/project.pbxproj`: `TARGETED_DEVICE_FAMILY = 1`, `MARKETING_VERSION = 1.0.0`

### Lệnh thường dùng

```bash
npm run native:sync   # build web + đồng bộ sang android/ và ios/
npm run android       # như trên rồi mở Android Studio
npm run ios           # như trên rồi mở Xcode
npm run assets        # sinh lại icon, màn hình chờ, hình cho store
```

### Hạn chế còn lại

- **Lịch sử ván đấu** nằm trong IndexedDB của WebView và chưa được sao sang kho native; nếu hệ điều hành dọn dữ liệu WebView thì
  lịch sử có thể mất (ván đang chơi, preset, vai trò tự tạo và cài đặt thì không). Bản sao lưu xuất tay vẫn chứa đủ lịch sử.
- **Ngăn xếp hoàn tác** không được sao sang kho native (có thể lớn); sau khi khôi phục từ kho native sẽ không hoàn tác được các
  bước trước đó.
- Ba trang công khai (quyền riêng tư, hỗ trợ, điều khoản) mới có tiếng Việt và tiếng Anh.
- Hồ sơ store mới viết sẵn tiếng Việt và tiếng Anh.
- Chưa có ảnh chụp màn hình cho store.
