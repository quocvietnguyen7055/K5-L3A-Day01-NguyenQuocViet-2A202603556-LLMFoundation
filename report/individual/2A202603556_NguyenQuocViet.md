# Báo cáo cá nhân — Day 01: Lọc tin nhắn rác bằng ML, DL, Embedding và LLM

- **MSSV:** 2A202603556
- **Họ và tên:** Nguyen Quoc Viet
- **SEED** (in ở ô đầu notebook): 8225

## 1. Bằng chứng

| Tệp | Có? |
| --- | --- |
| [`day01_lab.ipynb`](day01_lab.ipynb) — notebook đã chạy, còn output | ☑ (Phần 0–4; Phần 5 chưa chạy) |
| [`lab1_report.json`](lab1_report.json) — do ô "Báo cáo cuối" sinh ra | ☑ (10/10 kiểm tra ✅) |
| [`hand_calc.jpg`](hand_calc.jpg) — ảnh tính tay có các bước | ☐ (chưa làm) |

## 2. Kết quả chính

Số liệu lấy từ `lab1_report.json` (SEED 8225). LLM chạy qua xkiro (`qwen/qwen3.7-plus:free`, OpenAI-compatible), chỉ trên SUB 40 tin; 4a và 4b dùng **cùng một model** vì chỉ có một model miễn phí.

| Phương án | Precision | Recall | F1 (test) | F1 (SUB 40) | Train (s) | Tin/s (cả lô) | p50 ms/tin | p95 ms/tin | USD / 1k tin |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 1. BoW + LogReg | 0.988 | 0.823 | 0.898 | 0.857 | 9.5 | 12 058 | 0.05 | 0.12 | 0 |
| 2. BoW + MLP | 0.989 | 0.896 | 0.940 | 0.919 | 16.0 | 15 228 | 0.24 | 2.37 | 0 |
| 3a. MiniLM + kNN | 0.876 | 0.958 | 0.915 | 1.000 | 84.5 | 27 | 65.2 | 121.6 | 0 |
| 3b. MiniLM + LogReg | 0.979 | 0.969 | 0.974 | 1.000 | 84.9 | 36 | 26.4 | 32.4 | 0 |
| 3c. MiniLM + MLP head | 0.957 | 0.938 | 0.947 | 0.974 | 85.7 | 35 | 27.4 | 34.7 | 0 |
| 4a. LLM zero-shot (lần 1) | 0.933 | 0.700 | — | 0.800 | 0 | 0.14 | 6 139 | 12 447 | 0 (free) |
| 4b. LLM zero-shot (lần 2) | 0.950 | 0.950 | — | 0.950 | 0 | 0.14 | 5 268 | 13 620 | 0 (free) |
| 4c. LLM few-shot | 1.000 | 0.800 | — | 0.889 | 0 | 0.16 | 5 143 | 15 145 | 0 (free) |

## 3. Dự đoán và thực tế

*Chọn 3 dự đoán `predict(...)` lệch nhiều nhất so với kết quả. Mỗi cái: bạn đoán gì, ra gì, vì sao lệch.*

## 4. Phân tích 50 case khó

Chưa chạy stress test 50 case khó (không đủ thời gian).

## 5. Thử thách cá nhân

Chưa làm (không đủ thời gian).

## 6. Phương án cho sản phẩm thật

*Với yêu cầu p95 < 50 ms/tin cho 10 triệu SMS/ngày: chọn phương án nào, dẫn số liệu nào, chấp nhận đánh đổi gì.*

## 7. AI log và điều đã học

| Phần | Hỏi AI gì | AI trả lời / viết gì | Mình đã sửa / kiểm chứng gì |
| --- | --- | --- | --- |
| Cài đặt | Claude Code: đọc README, hướng dẫn mở Colab, đặt STUDENT_ID, cách nộp bài, sửa lỗi `git push` 403 | Hướng dẫn từng bước; chép notebook vào `report/individual/`, đổi tên file báo cáo | Tự làm theo trên Colab / GitHub |
| Phần 1–3 | Claude Code: giải thích TODO 1.1 (bag-of-words) | Chỉ giải thích khái niệm và các bước, không viết code | Tự viết code Phần 1–3 |
| Phần 4 | Claude Code: viết TODO 4.1–4.4 (`call_openai`, `build_classification_prompt`, `parse_label`, `llm_classify_batch`) | Code hoàn chỉnh cho 4 hàm | Kiểm tra `parse_label` xét "not spam" trước "spam"; chi phí ước tính theo số_từ / 0.75; 2 ô kiểm tra ✅ |
| Phần 4 | Claude Code: cấu hình provider xkiro (Qwen), sửa lỗi `Illegal header value` | Thêm mục `"xkiro"` vào `PROVIDERS` (base_url `https://api.xkiro.com/v1`, `max_tokens` 512); lỗi do key trong Secret có ký tự xuống dòng | Nhập lại key trong Colab Secrets, chạy lại 4.A / 4.B |

*Điều đã học (2–3 câu): …*
