# **ArtWiz-VersionHub**

## **Giới thiệu**
`ArtWiz-VersionHub` là repository chứa thông tin về các phiên bản của **ArtWiz**. Repository này được sử dụng để kiểm tra cập nhật từ ứng dụng ArtWiz thông qua **GitHub API**.

Có hai file quan trọng:
- **`latest-version.json`**: Lưu thông tin về phiên bản mới nhất.
- **`versions.json`**: Lưu danh sách tất cả các phiên bản đã phát hành.

## **Cấu trúc latest-version.json**
File `latest-version.json` lưu thông tin về phiên bản mới nhất của ArtWiz theo định dạng:

```json
{
  "latestVersion": "1.1.1.1",
  "downloadUrl": "https://artwiz.com/download",
  "releaseNotes": "Fix bugs and improve performance."
}
```

### **Giải thích các trường trong `latest-version.json`**
- `latestVersion`: Phiên bản mới nhất theo format **1.1.1.1**.
- `downloadUrl`: Link tải phiên bản mới.
- `releaseNotes`: Mô tả chi tiết về bản cập nhật.

## **Cấu trúc versions.json**
File `versions.json` lưu danh sách tất cả các phiên bản đã phát hành:

```json
[
  {
    "version": "1.1.1.1",
    "downloadUrl": "https://artwiz.com/download/1.1.1.1",
    "releaseNotes": "Fix minor bugs."
  },
  {
    "version": "1.1.1.0",
    "downloadUrl": "https://artwiz.com/download/1.1.1.0",
    "releaseNotes": "Added new feature."
  }
]
```

### **Giải thích các trường trong `versions.json`**
- `version`: Số phiên bản phát hành.
- `downloadUrl`: Link tải bản phát hành tương ứng.
- `releaseNotes`: Mô tả chi tiết về cập nhật của từng phiên bản.

## **Quy tắc nâng version trong ArtWiz**
Phiên bản của ArtWiz tuân theo format **X.Y.Z.W** (`1.1.1.1`), trong đó:
- `X` (**Major OS/WPF Upgrade**): Tăng khi có nâng cấp **hệ điều hành (OS)** hoặc **WPF framework**.
- `Y` (**Major Feature Update**): Tăng khi có tích hợp **tính năng lớn**.
- `Z` (**Minor Feature / Critical Fix**): Tăng khi có **tính năng nhỏ** hoặc **sửa lỗi nghiêm trọng**.
- `W` (**Minor Fix**): Tăng khi có **sửa lỗi nhỏ**.

### **Ví dụ về cách nâng version:**
| Phiên bản cũ | Phiên bản mới | Lý do nâng cấp |
|-------------|-------------|------------------------------|
| 1.1.1.1     | 2.0.0.0     | OS hoặc WPF framework được nâng cấp |
| 1.1.1.1     | 1.2.0.0     | Thêm tính năng lớn vào ArtWiz |
| 1.1.1.1     | 1.1.2.0     | Thêm một tính năng nhỏ hoặc sửa lỗi quan trọng |
| 1.1.1.1     | 1.1.1.2     | Sửa lỗi nhỏ không ảnh hưởng lớn |

## **Hướng dẫn cập nhật version**
1. **Cập nhật file `latest-version.json`** với thông tin phiên bản mới nhất.
2. **Thêm phiên bản mới vào `versions.json`** để lưu lại lịch sử phát hành.
3. Commit thay đổi với nội dung mô tả phiên bản.
4. Ứng dụng ArtWiz sẽ kiểm tra GitHub API và hiển thị thông báo cập nhật nếu có phiên bản mới.

## **Hướng dẫn lấy thông tin qua API**
Ứng dụng ArtWiz có thể kiểm tra phiên bản mới nhất bằng cách gửi HTTP GET request đến:

- **Lấy phiên bản mới nhất:**
  ```
  https://raw.githubusercontent.com/username/ArtWiz-VersionHub/main/latest-version.json
  ```

- **Lấy danh sách tất cả phiên bản đã phát hành:**
  ```
  https://raw.githubusercontent.com/username/ArtWiz-VersionHub/main/versions.json
  ```

### **Ví dụ sử dụng trong code (C#)**
```csharp
using System;
using System.Net.Http;
using System.Threading.Tasks;
using Newtonsoft.Json;

public class VersionChecker
{
    private static readonly HttpClient client = new HttpClient();
    
    public static async Task CheckLatestVersion()
    {
        string url = "https://raw.githubusercontent.com/username/ArtWiz-VersionHub/main/latest-version.json";
        var response = await client.GetStringAsync(url);
        var versionInfo = JsonConvert.DeserializeObject<dynamic>(response);
        Console.WriteLine($"Latest Version: {versionInfo.latestVersion}");
        Console.WriteLine($"Download URL: {versionInfo.downloadUrl}");
    }
}
```

