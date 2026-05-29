# Tổng hợp lệnh (Mục 2–5)

Bảng sau tổng hợp các lệnh từ mục **2 (NumPy)** tới **5 (Streamlit)** trong `MAIN_COMMANDS.md`.

| STT | Lệnh | Cú pháp | Ý nghĩa |
|---:|---|---|---|
| 1 | `np.mean` | `np.mean(X, axis=0)` | Tính khuôn mặt trung bình $\bar{x}=\frac{1}{N}\sum_{i=1}^N x_i$ theo từng pixel. |
| 2 | `X - mean_face` (broadcasting) | `X - mean_face` | Trung tâm hóa: $\Phi_i = x_i - \bar{x}$ (tự động trừ `mean_face` cho mọi hàng). |
| 3 | `@` / `np.matmul` | `Phi @ Phi.T`, `Phi.T @ V`, `(X - mean_face) @ U` | Nhân ma trận — dùng cho $L=(\Phi\Phi^T)/N$, khôi phục eigenfaces và phép chiếu. |
| 4 | `.T` | `Phi.T` | Chuyển vị ma trận (đổi hàng ↔ cột). |
| 5 | `np.linalg.eigh` | `np.linalg.eigh(L)` | Phân rã trị riêng của ma trận đối xứng — trả về (eigenvalues, eigenvectors). |
| 6 | `np.argsort` | `np.argsort(arr)[::-1]` | Sắp xếp indices theo trị riêng giảm dần để chọn k eigenfaces quan trọng nhất. |
| 7 | `np.linalg.norm` | `np.linalg.norm(U, axis=0)` | Tính norm theo cột để chuẩn hóa eigenfaces về độ dài 1 (orthonormal). |
| 8 | Tính khoảng cách Euclidean | `np.sqrt(np.sum(diffs**2, axis=1))` | Tính khoảng cách Euclidean $\lVert\hat{y}-\hat{y}_i\rVert_2$ trong không gian eigenface. |
| 9 | `np.argmin` | `np.argmin(distances)` | Tìm chỉ số có khoảng cách nhỏ nhất (1‑NN). |
| 10 | `np.clip` | `np.clip(X, 0, 255)` | Cắt giá trị pixel về dải hợp lệ `[0,255]` sau tái tạo. |
| 11 | `np.cumsum` / `np.searchsorted` | `np.cumsum(ratio)` / `np.searchsorted(cumvar, 0.95)` | Tính phương sai tích lũy và tìm `k` tối thiểu đạt 95% phương sai. |
| 12 | `.reshape` | `.reshape(112, 92)` | Chuyển vector 1D `(10304,)` → ảnh 2D `(112,92)` để hiển thị. |
| 13 | `.flatten()` | `img.flatten()` | Vector hóa ảnh: chuyển ảnh 2D → vector 1D (chuẩn bị cho đại số tuyến tính). |
| 14 | Tính accuracy | `np.mean(y_true == y_pred)` | Tính độ chính xác bằng trung bình của biểu thức boolean (True=1, False=0). |
| 15 | `Image.open` | `Image.open(path)` | Mở file ảnh (`.pgm`, `.jpg`, `.png`). |
| 16 | `img.convert("L")` | `img.convert("L")` | Chuyển ảnh sang grayscale 8‑bit (0–255). |
| 17 | `img.resize` | `img.resize((92, 112))` | Đổi kích thước về chuẩn ORL để mọi vector cùng độ dài. |
| 18 | `np.array(img, dtype=np.float64)` | `np.array(img, dtype=np.float64)` | Chuyển ảnh PIL → mảng NumPy `float64` cho đại số tuyến tính. |
| 19 | `plt.subplots` | `plt.subplots(figsize=...)` | Tạo `figure` và `axes` — khung cho các biểu đồ. |
| 20 | `ax.imshow` | `ax.imshow(img, cmap='gray', vmin=0, vmax=255)` | Hiển thị mean face và eigenfaces dưới dạng ảnh xám. |
| 21 | `ax.plot` | `ax.plot(k_values, accuracies, marker='o')` | Vẽ đường Accuracy theo `k`. |
| 22 | `ax.bar` | `ax.bar(indices, evr)` | Vẽ cột phương sai từng eigenface. |
| 23 | `ax.axhline` | `ax.axhline(y=95, linestyle='--')` | Vẽ ngưỡng 95% phương sai. |
| 24 | `ax.twinx` | `ax.twinx()` | Tạo trục y thứ hai cho biểu đồ kép (phương sai tích lũy). |
| 25 | `ax.annotate` | `ax.annotate("k tốt nhất", xy=..., arrowprops=...)` | Chú thích có mũi tên chỉ vào điểm `k` tối ưu. |
| 26 | `fig.savefig` | `fig.savefig(path, dpi=150, bbox_inches='tight')` | Lưu figure ra PNG cho báo cáo. |
| 27 | `plt.close` | `plt.close(fig)` | Đóng figure để giải phóng bộ nhớ. |
| 28 | `st.set_page_config` | `st.set_page_config(page_title=..., layout="wide")` | Cấu hình trang Streamlit (tiêu đề, layout). |
| 29 | `st.title / st.markdown` | `st.title(...); st.markdown(...)` | Tiêu đề và nội dung markdown trên giao diện. |
| 30 | `st.columns` | `st.columns(2)` | Chia layout thành 2 cột (ví dụ: ảnh trước / sau). |
| 31 | `st.tabs` | `st.tabs([...])` | Tạo các tab chuyển giữa các bước/khung nhìn. |
| 32 | `st.slider` | `st.slider("k", 5, 150, 50)` | Thanh trượt cho người dùng chọn số eigenfaces `k`. |
| 33 | `st.file_uploader` | `st.file_uploader("Upload", type=["jpg","png"])` | Cho phép upload ảnh để nhận dạng thử. |
| 34 | `st.image` | `st.image(arr, caption=...)` | Hiển thị ảnh (mean face, eigenfaces, ảnh tái tạo...). |
| 35 | `st.metric` | `st.metric("Accuracy", "...")` | Hiển thị chỉ số nổi bật (ví dụ: Accuracy). |
| 36 | `@st.cache_data / @st.cache_resource` | `@st.cache_data` hoặc `@st.cache_resource` | Cache dataset và mô hình đã huấn luyện để tránh tính lại. |
| 37 | `st.session_state` | `st.session_state` | Lưu trạng thái mô hình/biến giữa các lần rerun. |

