# The OAuth 2.0 Authorization Framework RFC6749
***Hardt, D., Ed., ["The OAuth 2.0 Authorization Framework"](https://www.rfc-editor.org/info/rfc6749), RFC 6749, DOI 10.17487/RFC6749(), October 2012.***

**Disclaimer: This is a Vietnamese translated version containing key content from the original document and is provided for personal study purposes only. It is not a complete version of the document. For accurate and comprehensive information, please refer to [the original document](https://www.rfc-editor.org/info/rfc6749).**
- [The OAuth 2.0 Authorization Framework RFC6749](#the-oauth-20-authorization-framework-rfc6749)
  - [1. Introduction](#1-introduction)
    - [1.1. Roles](#11-roles)
    - [1.2. **Protocol Flow**](#12-protocol-flow)
    - [1.3. Authorization Grant](#13-authorization-grant)
      - [1.3.1. Authorization Code](#131-authorization-code)
      - [1.3.2. Implicit](#132-implicit)
      - [1.3.3. Resource Owner Password Credentials](#133-resource-owner-password-credentials)
      - [1.3.4. Client Credentials](#134-client-credentials)
    - [1.4. Access Token](#14-access-token)
    - [1.5. Refresh Token](#15-refresh-token)
    - [1.6. TLS Version](#16-tls-version)
    - [1.7. HTTP Redirections](#17-http-redirections)
    - [1.8. Interoperability](#18-interoperability)
    - [1.9. Notational Conventions](#19-notational-conventions)
  - [2. Client Registration](#2-client-registration)
    - [2.1. Client Types](#21-client-types)
    - [2.2. Client Identifier](#22-client-identifier)
    - [2.3. Client Authentication](#23-client-authentication)
      - [2.3.1. Client Password](#231-client-password)
      - [2.3.2. Other Authentication Methods](#232-other-authentication-methods)
    - [2.4. Unregistered Clients](#24-unregistered-clients)
  - [3. Protocol Endpoints](#3-protocol-endpoints)
    - [3.1. Authorization Endpoint](#31-authorization-endpoint)
      - [3.1.1. Response Type](#311-response-type)
      - [3.1.2. Redirection Endpoint](#312-redirection-endpoint)
        - [3.1.2.1. Endpoint Request Confidentiality](#3121-endpoint-request-confidentiality)
        - [3.1.2.2. Registration Requirements](#3122-registration-requirements)
        - [3.1.2.3. Dynamic Configuration](#3123-dynamic-configuration)
        - [3.1.2.4. Invalid Endpoint](#3124-invalid-endpoint)
        - [3.1.2.5. Endpoint Content](#3125-endpoint-content)
    - [3.2. Token Endpoint](#32-token-endpoint)
      - [3.2.1. Client Authentication](#321-client-authentication)
    - [3.3. Access Token Scope](#33-access-token-scope)
  - [4. Obtaining Authorization](#4-obtaining-authorization)
    - [4.1. Authorization Code Grant](#41-authorization-code-grant)
      - [4.1.1. Authorization Request](#411-authorization-request)
      - [4.1.2. Authorization Response](#412-authorization-response)
        - [4.1.2.1. Error Response](#4121-error-response)
      - [4.1.3. Access Token Request](#413-access-token-request)
      - [4.1.4. Access Token Response](#414-access-token-response)
- [](#)
    - [4.2. Implicit Grant](#42-implicit-grant)
      - [4.2.1. Authorization Request](#421-authorization-request)
      - [4.2.2. Access Token Response](#422-access-token-response)
        - [4.2.2.1. Error Response](#4221-error-response)
    - [4.3. Resource Owner Password Credentials Grant](#43-resource-owner-password-credentials-grant)
      - [4.3.1. Authorization Request and Response](#431-authorization-request-and-response)
      - [4.3.2. Access Token Request](#432-access-token-request)
      - [4.3.3. Access Token Response](#433-access-token-response)
- [](#-1)
    - [4.4. Client Credentials Grant](#44-client-credentials-grant)
      - [4.4.1. Authorization Request and Response](#441-authorization-request-and-response)
      - [4.4.2. Access Token Request](#442-access-token-request)
      - [4.4.3. Access Token Response](#443-access-token-response)
- [](#-2)
    - [4.5. Extension Grants](#45-extension-grants)
  - [5. Issuing an Access Token](#5-issuing-an-access-token)
    - [5.1. Successful Response](#51-successful-response)
    - [5.2. Error Response](#52-error-response)
  - [6. Refreshing an Access Token](#6-refreshing-an-access-token)
  - [7. Accessing Protected Resources](#7-accessing-protected-resources)
    - [7.1. Access Token Types](#71-access-token-types)
    - [7.2. Error Response](#72-error-response)
  - [8. Extensibility](#8-extensibility)
    - [8.1. Defining Access Token Types](#81-defining-access-token-types)
    - [8.2. Defining New Endpoint Parameters](#82-defining-new-endpoint-parameters)
    - [8.3. Defining New Authorization Grant Types](#83-defining-new-authorization-grant-types)
    - [8.4. Defining New Authorization Endpoint Response Types](#84-defining-new-authorization-endpoint-response-types)
    - [8.5. Defining Additional Error Codes](#85-defining-additional-error-codes)
  - [9. Native Applications](#9-native-applications)
  - [10. Security Considerations](#10-security-considerations)
    - [10.1. Client Authentication](#101-client-authentication)
    - [10.2. Client Impersonation](#102-client-impersonation)
    - [10.3. Access Tokens](#103-access-tokens)
    - [10.4. Refresh Tokens](#104-refresh-tokens)
    - [10.5. Authorization Codes](#105-authorization-codes)
    - [10.6. Thao Tác URI Chuyển Hướng Mã Ủy Quyền (Authorization Code Redirection URI Manipulation)](#106-thao-tác-uri-chuyển-hướng-mã-ủy-quyền-authorization-code-redirection-uri-manipulation)
    - [10.7. Resource Owner Password Credentials](#107-resource-owner-password-credentials)
    - [10.8. Yêu Cầu Bảo Mật (Request Confidentiality)](#108-yêu-cầu-bảo-mật-request-confidentiality)
    - [10.9. Đảm Bảo Tính Xác Thực của Endpoint (Ensuring Endpoint Authenticity)](#109-đảm-bảo-tính-xác-thực-của-endpoint-ensuring-endpoint-authenticity)
    - [10.10. Tấn Công Đoán Credentials (Credentials-Guessing Attacks)](#1010-tấn-công-đoán-credentials-credentials-guessing-attacks)
    - [10.11. Tấn Công Lừa Đảo (Phishing Attacks)](#1011-tấn-công-lừa-đảo-phishing-attacks)
    - [10.12. Tấn Công Giả Mạo Yêu Cầu Đa Trang (Cross-Site Request Forgery)](#1012-tấn-công-giả-mạo-yêu-cầu-đa-trang-cross-site-request-forgery)
    - [10.13. Clickjacking](#1013-clickjacking)
    - [10.14. Tiêm Mã và Xác Thực Đầu Vào (Code Injection and Input Validation)](#1014-tiêm-mã-và-xác-thực-đầu-vào-code-injection-and-input-validation)
    - [10.15. Trình Chuyển Hướng Mở (Open Redirectors)](#1015-trình-chuyển-hướng-mở-open-redirectors)
    - [10.16. Lạm Dụng Access Token để Mạo Danh Resource Owner trong Luồng Implicit (Misuse of Access Token to Impersonate Resource Owner in Implicit Flow)](#1016-lạm-dụng-access-token-để-mạo-danh-resource-owner-trong-luồng-implicit-misuse-of-access-token-to-impersonate-resource-owner-in-implicit-flow)
  - [11. IANA Considerations](#11-iana-considerations)
    - [11.1. OAuth Access Token Types Registry](#111-oauth-access-token-types-registry)
      - [11.1.1. Registration Template](#1111-registration-template)
      - [11.2. OAuth Parameters Registry](#112-oauth-parameters-registry)
      - [11.2.1. Registration Template](#1121-registration-template)
      - [11.2.2. Initial Registry Contents](#1122-initial-registry-contents)
    - [11.3. OAuth Authorization Endpoint Response Types Registry](#113-oauth-authorization-endpoint-response-types-registry)
      - [11.3.1. Registration Template](#1131-registration-template)
      - [11.3.2. Initial Registry Contents](#1132-initial-registry-contents)
    - [11.4. OAuth Extensions Error Registry](#114-oauth-extensions-error-registry)
      - [11.4.1. Registration Template](#1141-registration-template)


## 1. Introduction

### 1.1. Roles

OAuth định nghĩa bốn vai trò:

- resource owner
    
    Một thực thể có khả năng cấp quyền truy cập vào một resource được bảo vệ. Khi resource owner là một người, nó được gọi là một end-user.
    
- resource server
    
    Máy chủ lưu trữ các protected resources, có khả năng chấp nhận và phản hồi các protected resource requests bằng cách sử dụng access tokens.
    
- client
    
    Một ứng dụng thực hiện protected resource requests thay mặt cho resource owner và với sự ủy quyền của họ. Thuật ngữ "client" không ngụ ý bất kỳ đặc điểm triển khai cụ thể nào (ví dụ: liệu ứng dụng chạy trên máy chủ, máy tính để bàn hay các thiết bị khác).
    
- authorization server
    
    Máy chủ cấp access tokens cho client sau khi xác thực thành công resource owner và nhận được sự ủy quyền.
    

Sự tương tác giữa authorization server và resource server nằm ngoài phạm vi của đặc tả này. authorization server có thể là cùng một máy chủ với resource server hoặc một thực thể riêng biệt. Một authorization server duy nhất có thể cấp access tokens được chấp nhận bởi nhiều resource servers.

---

### 1.2. **Protocol Flow**

     `+--------+                               +---------------+
     |        |--(A)- Authorization Request ->|   Resource    |
     |        |                               |     Owner     |
     |        |<-(B)-- Authorization Grant ---|               |
     |        |                               +---------------+
     |        |
     |        |                               +---------------+
     |        |--(C)-- Authorization Grant -->| Authorization |
     | Client |                               |     Server    |
     |        |<-(D)----- Access Token -------|               |
     |        |                               +---------------+
     |        |
     |        |                               +---------------+
     |        |--(E)----- Access Token ------>|    Resource   |
     |        |                               |     Server    |
     |        |<-(F)--- Protected Resource ---|               |
     +--------+                               +---------------+

                     Figure 1: Abstract Protocol Flow`

Luồng OAuth 2.0 trừu tượng được minh họa trong Hình 1 mô tả sự tương tác giữa bốn vai trò và bao gồm các bước sau:

(A) **Client** yêu cầu ủy quyền từ **resource owner**. Yêu cầu ủy quyền có thể được thực hiện trực tiếp đến **resource owner** (như được hiển thị), hoặc tốt hơn là gián tiếp thông qua **authorization server** như một trung gian.

(B) **Client** nhận được một **authorization grant**, đây là một thông tin xác thực thể hiện sự ủy quyền của **resource owner**, được thể hiện bằng một trong bốn **grant types** được định nghĩa trong đặc tả này hoặc sử dụng một **extension grant type**. Loại **authorization grant** phụ thuộc vào phương pháp được **client** sử dụng để yêu cầu ủy quyền và các loại được **authorization server** hỗ trợ.

(C) **Client** yêu cầu một **access token** bằng cách xác thực với **authorization server** và trình bày **authorization grant**.

(D) **Authorization server** xác thực **client** và xác nhận **authorization grant**, và nếu hợp lệ, cấp một **access token**.

(E) **Client** yêu cầu **protected resource** từ **resource server** và xác thực bằng cách trình bày **access token**.

(F) **Resource server** xác nhận **access token**, và nếu hợp lệ, phục vụ yêu cầu.

Phương pháp ưu tiên để **client** lấy **authorization grant** từ **resource owner** (được mô tả trong các bước (A) và (B)) là sử dụng **authorization server** làm trung gian, được minh họa trong Hình 3 trong Phần 4.1.

---

### 1.3. Authorization Grant

Authorization grant là một loại thông tin xác thực đại diện cho sự cho phép của resource owner (người sở hữu tài nguyên) nhằm truy cập các tài nguyên được bảo vệ. Thông tin này được client sử dụng để lấy access token. Tài liệu này định nghĩa bốn loại grant — *authorization code*, *implicit*, *resource owner password credentials*, và *client credentials* — cũng như một cơ chế mở rộng để định nghĩa thêm các loại khác.

---

#### 1.3.1. Authorization Code

Authorization code được lấy thông qua việc sử dụng authorization server như một trung gian giữa client và resource owner. Thay vì yêu cầu sự cho phép trực tiếp từ resource owner, client sẽ chuyển hướng resource owner đến authorization server (thông qua user-agent của họ như được định nghĩa trong [RFC2616]), và sau đó authorization server sẽ chuyển resource owner trở lại client kèm theo authorization code.

Trước khi chuyển hướng resource owner trở lại client với authorization code, authorization server sẽ xác thực resource owner và lấy sự cho phép. Vì resource owner chỉ xác thực với authorization server nên thông tin xác thực của họ sẽ không bao giờ bị chia sẻ với client.

Authorization code cung cấp một số lợi ích bảo mật quan trọng, chẳng hạn như khả năng xác thực client, cũng như việc truyền access token trực tiếp đến client mà không phải đi qua user-agent của resource owner – điều này giúp hạn chế khả năng token bị lộ cho người khác, bao gồm cả resource owner.

---

#### 1.3.2. Implicit

Implicit grant là một dạng đơn giản hóa của authorization code flow, được tối ưu cho các client được triển khai trong trình duyệt sử dụng ngôn ngữ kịch bản như JavaScript. Trong implicit flow, thay vì cấp authorization code cho client, client sẽ được cấp trực tiếp một access token (là kết quả của việc resource owner cấp quyền).

Grant type này được gọi là *implicit* vì không có thông tin xác thực trung gian nào (chẳng hạn như authorization code) được cấp và sử dụng sau đó để lấy access token.

Khi cấp access token trong implicit flow, authorization server không xác thực client. Trong một số trường hợp, danh tính của client có thể được xác minh thông qua redirection URI được sử dụng để gửi access token về client. Access token có thể bị lộ cho resource owner hoặc các ứng dụng khác có quyền truy cập vào user-agent của resource owner.

Implicit grant cải thiện khả năng phản hồi và hiệu quả cho một số client (ví dụ: client được xây dựng như một ứng dụng chạy trong trình duyệt), vì nó giảm số vòng trao đổi cần thiết để lấy access token. Tuy nhiên, sự thuận tiện này cần được cân nhắc với các rủi ro bảo mật khi sử dụng implicit grant, như mô tả trong các Mục 10.3 và 10.16, đặc biệt là khi loại grant *authorization code* khả dụng.

---

#### 1.3.3. Resource Owner Password Credentials

Resource owner password credentials (ví dụ: username và password) có thể được sử dụng trực tiếp như một authorization grant để lấy access token. Các thông tin xác thực này chỉ nên được sử dụng khi có mức độ tin tưởng cao giữa resource owner và client (ví dụ: client là một phần của hệ điều hành thiết bị hoặc là một ứng dụng có quyền cao), và khi các loại authorization grant khác không khả dụng (như authorization code).

Mặc dù loại grant này yêu cầu client truy cập trực tiếp vào thông tin xác thực của resource owner, nhưng thông tin này chỉ được sử dụng cho một yêu cầu duy nhất và sẽ được trao đổi để lấy access token. Grant type này giúp loại bỏ nhu cầu lưu trữ thông tin xác thực của resource owner cho các lần sử dụng sau, bằng cách trao đổi thông tin đó với access token có thời gian sống dài hoặc refresh token.

---

#### 1.3.4. Client Credentials

Client credentials (hoặc các hình thức xác thực client khác) có thể được sử dụng như một authorization grant khi phạm vi ủy quyền chỉ giới hạn trong các tài nguyên được bảo vệ dưới quyền kiểm soát của client, hoặc với các tài nguyên đã được sắp xếp trước với authorization server. Client credentials thường được sử dụng như một authorization grant khi client hoạt động thay mặt chính nó (client đồng thời là resource owner), hoặc khi client yêu cầu truy cập vào tài nguyên được bảo vệ dựa trên một ủy quyền đã được sắp xếp trước với authorization server.

---

---

### 1.4. Access Token

**Access tokens** là các credentials được sử dụng để truy cập các **protected resources**. Một **access token** là một chuỗi đại diện cho quyền ủy quyền được cấp cho **client**. Chuỗi này thường là **opaque** đối với **client**. Các tokens đại diện cho các **scopes** và thời lượng truy cập cụ thể, được cấp bởi **resource owner** và được thực thi bởi **resource server** và **authorization server**.

Token có thể biểu thị một **identifier** được sử dụng để truy xuất thông tin ủy quyền hoặc có thể tự chứa thông tin ủy quyền một cách có thể xác minh được (tức là một chuỗi token bao gồm một số dữ liệu và một **signature**). Các credentials xác thực bổ sung, nằm ngoài phạm vi của đặc tả này, có thể được yêu cầu để **client** sử dụng token.

**Access token** cung cấp một lớp trừu tượng, thay thế các cấu trúc ủy quyền khác nhau (ví dụ: username và password) bằng một token duy nhất được **resource server** hiểu. Sự trừu tượng này cho phép cấp **access tokens** có tính hạn chế hơn so với **authorization grant** được sử dụng để lấy chúng, cũng như loại bỏ nhu cầu **resource server** phải hiểu nhiều phương thức xác thực khác nhau.

**Access tokens** có thể có các định dạng, cấu trúc và phương pháp sử dụng khác nhau (ví dụ: các thuộc tính mã hóa) dựa trên các yêu cầu bảo mật của **resource server**. Các thuộc tính của **access token** và các phương pháp được sử dụng để truy cập **protected resources** nằm ngoài phạm vi của đặc tả này và được định nghĩa bởi các đặc tả đi kèm như [RFC6750].

---

### 1.5. Refresh Token

**Refresh tokens** là các credentials được sử dụng để lấy **access tokens**. **Refresh tokens** được **authorization server** cấp cho **client** và được sử dụng để lấy một **access token** mới khi **access token** hiện tại trở nên không hợp lệ hoặc hết hạn, hoặc để lấy các **access tokens** bổ sung với cùng **scope** hoặc **scope** hẹp hơn (**access tokens** có thể có thời gian tồn tại ngắn hơn và ít quyền hơn so với quyền được **resource owner** cấp). Việc cấp một **refresh token** là tùy chọn theo quyết định của **authorization server**. Nếu **authorization server** cấp một **refresh token**, nó sẽ được bao gồm khi cấp một **access token** (tức là bước (D) trong Hình 1).

Một **refresh token** là một chuỗi đại diện cho quyền ủy quyền được cấp cho **client** bởi **resource owner**. Chuỗi này thường là **opaque** đối với **client**. Token biểu thị một **identifier** được sử dụng để truy xuất thông tin ủy quyền. Không giống như **access tokens**, **refresh tokens** chỉ được sử dụng với **authorization servers** và không bao giờ được gửi đến **resource servers**.
```
  +--------+                                           +---------------+
  |        |--(A)------- Authorization Grant --------->|               |
  |        |                                           |               |
  |        |<-(B)----------- Access Token -------------|               |
  |        |               & Refresh Token             |               |
  |        |                                           |               |
  |        |                            +----------+   |               |
  |        |--(C)---- Access Token ---->|          |   |               |
  |        |                            |          |   |               |
  |        |<-(D)- Protected Resource --| Resource |   | Authorization |
  | Client |                            |  Server  |   |     Server    |
  |        |--(E)---- Access Token ---->|          |   |               |
  |        |                            |          |   |               |
  |        |<-(F)- Invalid Token Error -|          |   |               |
  |        |                            +----------+   |               |
  |        |                                           |               |
  |        |--(G)----------- Refresh Token ----------->|               |
  |        |                                           |               |
  |        |<-(H)----------- Access Token -------------|               |
  +--------+           & Optional Refresh Token        +---------------+
```
               Figure 2: Refreshing an Expired Access Token

Luồng minh họa trong Hình 2 bao gồm các bước sau:

(A) **Client** yêu cầu một **access token** bằng cách xác thực với **authorization server** và trình bày một **authorization grant**.

(B) **Authorization server** xác thực **client** và xác nhận **authorization grant**, và nếu hợp lệ, cấp một **access token** và một **refresh token**.

(C) **Client** thực hiện một **protected resource request** đến **resource server** bằng cách trình bày **access token**.

(D) **Resource server** xác nhận **access token**, và nếu hợp lệ, phục vụ yêu cầu.

(E) Các bước (C) và (D) lặp lại cho đến khi **access token** hết hạn. Nếu **client** biết **access token** đã hết hạn, nó sẽ bỏ qua đến bước (G); ngược lại, nó thực hiện một **protected resource request** khác.

(F) Vì **access token** không hợp lệ, **resource server** trả về lỗi **invalid token error**.

(G) **Client** yêu cầu một **access token** mới bằng cách xác thực với **authorization server** và trình bày **refresh token**. Các yêu cầu xác thực **client** dựa trên loại **client** và các chính sách của **authorization server**.

(H) **Authorization server** xác thực **client** và xác nhận **refresh token**, và nếu hợp lệ, cấp một **access token** mới (và, tùy chọn, một **refresh token** mới).

Các bước (C), (D), (E) và (F) nằm ngoài phạm vi của đặc tả này, như được mô tả trong Phần 7.

---

### 1.6. TLS Version

Bất cứ khi nào **Transport Layer Security (TLS)** được đặc tả này sử dụng, phiên bản (hoặc các phiên bản) **TLS** thích hợp sẽ thay đổi theo thời gian, dựa trên việc triển khai rộng rãi và các lỗ hổng bảo mật đã biết. Tại thời điểm viết bài này, **TLS** phiên bản 1.2 [RFC5246] là phiên bản mới nhất, nhưng có cơ sở triển khai rất hạn chế và có thể không dễ dàng có sẵn để triển khai. **TLS** phiên bản 1.0 [RFC2246] là phiên bản được triển khai rộng rãi nhất và sẽ cung cấp khả năng tương tác rộng nhất.

Các triển khai CÓ THỂ cũng hỗ trợ các cơ chế bảo mật lớp vận chuyển bổ sung đáp ứng yêu cầu bảo mật của chúng.

---

### 1.7. HTTP Redirections

Đặc tả này sử dụng rộng rãi các **HTTP redirections**, trong đó **client** hoặc **authorization server** điều hướng **user-agent** của **resource owner** đến một đích khác. Mặc dù các ví dụ trong đặc tả này cho thấy việc sử dụng mã trạng thái **HTTP 302**, bất kỳ phương pháp nào khác có sẵn thông qua **user-agent** để thực hiện việc chuyển hướng này đều được phép và được coi là một chi tiết triển khai.

---

### 1.8. Interoperability

OAuth 2.0 cung cấp một framework ủy quyền phong phú với các thuộc tính bảo mật được xác định rõ ràng. Tuy nhiên, với tư cách là một framework phong phú và có khả năng mở rộng cao với nhiều thành phần tùy chọn, bản thân đặc tả này có khả năng tạo ra một loạt các triển khai không tương thích.

Ngoài ra, đặc tả này để lại một vài thành phần bắt buộc được xác định một phần hoặc hoàn toàn không xác định (ví dụ: **client registration**, **authorization server capabilities**, **endpoint discovery**). Nếu không có các thành phần này, **clients** phải được cấu hình thủ công và cụ thể cho một **authorization server** và **resource server** cụ thể để có thể tương tác.

Framework này được thiết kế với kỳ vọng rõ ràng rằng công việc trong tương lai sẽ định nghĩa các **prescriptive profiles** và **extensions** cần thiết để đạt được khả năng tương tác web quy mô đầy đủ.

---

### 1.9. Notational Conventions

Các từ khóa "**MUST**", "**MUST NOT**", "**REQUIRED**", "**SHALL**", "**SHALL NOT**", "**SHOULD**", "**SHOULD NOT**", "**RECOMMENDED**", "**MAY**", và "**OPTIONAL**" trong đặc tả này được hiểu như mô tả trong [RFC2119].

Đặc tả này sử dụng ký hiệu **Augmented Backus-Naur Form (ABNF)** của [RFC5234]. Ngoài ra, quy tắc **URI-reference** được bao gồm từ "Uniform Resource Identifier (URI): Generic Syntax" [RFC3986].

Một số thuật ngữ liên quan đến bảo mật được hiểu theo nghĩa được định nghĩa trong [RFC4949]. Các thuật ngữ này bao gồm, nhưng không giới hạn ở, "**attack**", "**authentication**", "**authorization**", "**certificate**", "**confidentiality**", "**credential**", "**encryption**", "**identity**", "**sign**", "**signature**", "**trust**", "**validate**", và "**verify**".

Trừ khi có ghi chú khác, tất cả các tên và giá trị tham số **protocol** đều phân biệt chữ hoa, chữ thường.

---

## 2. Client Registration

Trước khi khởi tạo giao thức, **client** đăng ký với **authorization server**. Các phương tiện mà **client** đăng ký với **authorization server** nằm ngoài phạm vi của đặc tả này nhưng thường liên quan đến tương tác của **end-user** với một biểu mẫu đăng ký **HTML**.

Đăng ký **client** không yêu cầu tương tác trực tiếp giữa **client** và **authorization server**. Khi được **authorization server** hỗ trợ, việc đăng ký có thể dựa vào các phương tiện khác để thiết lập lòng tin và có được các **client properties** cần thiết (ví dụ: **redirection URI**, **client type**). Ví dụ, việc đăng ký có thể được thực hiện bằng cách sử dụng một **self-issued** hoặc **third-party-issued assertion**, hoặc bằng cách **authorization server** thực hiện **client discovery** bằng cách sử dụng một **trusted channel**.

Khi đăng ký một **client**, **client developer** SẼ:

- chỉ định **client type** như mô tả trong Phần 2.1,
- cung cấp các **client redirection URIs** của nó như mô tả trong Phần 3.1.2, và
- bao gồm bất kỳ thông tin nào khác được **authorization server** yêu cầu (ví dụ: tên ứng dụng, trang web, mô tả, hình ảnh logo, việc chấp nhận các điều khoản pháp lý).

---

### 2.1. Client Types

OAuth định nghĩa hai **client types**, dựa trên khả năng xác thực an toàn với **authorization server** (tức là khả năng duy trì tính bảo mật của **client credentials** của chúng):

- confidential
    
    Các clients có khả năng duy trì tính bảo mật của credentials của chúng (ví dụ: client được triển khai trên một secure server với quyền truy cập hạn chế vào client credentials), hoặc có khả năng xác thực client an toàn bằng các phương tiện khác.
    
- public
    
    Các clients không có khả năng duy trì tính bảo mật của credentials của chúng (ví dụ: các clients thực thi trên thiết bị được resource owner sử dụng, chẳng hạn như một installed native application hoặc một web browser-based application), và không có khả năng xác thực client an toàn thông qua bất kỳ phương tiện nào khác.
    

Việc chỉ định **client type** dựa trên định nghĩa của **authorization server** về xác thực an toàn và mức độ phơi bày **client credentials** chấp nhận được của nó. **Authorization server KHÔNG NÊN** đưa ra các giả định về **client type**.

Một **client** có thể được triển khai như một tập hợp các thành phần phân tán, mỗi thành phần có một **client type** và **security context** khác nhau (ví dụ: một **distributed client** với cả thành phần **confidential server-based** và thành phần **public browser-based**). Nếu **authorization server** không cung cấp hỗ trợ cho các **clients** như vậy hoặc không cung cấp hướng dẫn liên quan đến việc đăng ký của chúng, **client NÊN** đăng ký mỗi thành phần như một **client** riêng biệt.

Đặc tả này được thiết kế dựa trên các **client profiles** sau:

- web application
    
    Một web application là một confidential client chạy trên một web server. Resource owners truy cập client thông qua một HTML user interface được hiển thị trong một user-agent trên thiết bị được resource owner sử dụng. Các client credentials cũng như bất kỳ access token nào được cấp cho client được lưu trữ trên web server và không bị lộ hoặc không thể truy cập bởi resource owner.
    
- user-agent-based application
    
    Một user-agent-based application là một public client trong đó client code được tải xuống từ một web server và thực thi trong một user-agent (ví dụ: web browser) trên thiết bị được resource owner sử dụng. Dữ liệu protocol và credentials dễ dàng truy cập (và thường hiển thị) đối với resource owner. Vì các ứng dụng như vậy nằm trong user-agent, chúng có thể sử dụng liền mạch các khả năng của user-agent khi yêu cầu ủy quyền.
    
- native application
    
    Một native application là một public client được cài đặt và thực thi trên thiết bị được resource owner sử dụng. Dữ liệu protocol và credentials có thể truy cập được đối với resource owner. Người ta giả định rằng bất kỳ client authentication credentials nào được bao gồm trong ứng dụng đều có thể được trích xuất. Mặt khác, các credentials được cấp động như access tokens hoặc refresh tokens có thể nhận được một mức độ bảo vệ chấp nhận được. Tối thiểu, các credentials này được bảo vệ khỏi các hostile servers mà ứng dụng có thể tương tác. Trên một số nền tảng, các credentials này có thể được bảo vệ khỏi các ứng dụng khác nằm trên cùng thiết bị.
    

---

### 2.2. Client Identifier

**Authorization server** cấp cho **client** đã đăng ký một **client identifier** -- một chuỗi duy nhất đại diện cho thông tin đăng ký được cung cấp bởi **client**. **Client identifier** không phải là một bí mật; nó được hiển thị cho **resource owner** và **KHÔNG ĐƯỢC** sử dụng một mình để xác thực **client**. **Client identifier** là duy nhất đối với **authorization server**.

Kích thước chuỗi **client identifier** không được định nghĩa bởi đặc tả này. **Client** nên tránh đưa ra các giả định về kích thước **identifier**. **Authorization server NÊN** ghi lại kích thước của bất kỳ **identifier** nào mà nó cấp.

---

### 2.3. Client Authentication

Nếu **client type** là **confidential**, **client** và **authorization server** thiết lập một phương thức xác thực **client** phù hợp với yêu cầu bảo mật của **authorization server**. **Authorization server CÓ THỂ** chấp nhận bất kỳ hình thức xác thực **client** nào đáp ứng yêu cầu bảo mật của nó.

Các **confidential clients** thường được cấp (hoặc thiết lập) một bộ **client credentials** được sử dụng để xác thực với **authorization server** (ví dụ: **password**, cặp khóa **public/private key**).

**Authorization server CÓ THỂ** thiết lập một phương thức xác thực **client** với các **public clients**. Tuy nhiên, **authorization server KHÔNG ĐƯỢC** dựa vào xác thực **public client** cho mục đích nhận dạng **client**.

**Client KHÔNG ĐƯỢC** sử dụng nhiều hơn một phương thức xác thực trong mỗi request.

#### 2.3.1. Client Password

Các **clients** sở hữu một **client password CÓ THỂ** sử dụng lược đồ xác thực **HTTP Basic** như được định nghĩa trong [RFC2617] để xác thực với **authorization server**. **Client identifier** được mã hóa bằng thuật toán mã hóa "**application/x-www-form-urlencoded**" theo Phụ lục B, và giá trị được mã hóa được sử dụng làm **username**; **client password** được mã hóa bằng cùng thuật toán và được sử dụng làm **password**. **Authorization server PHẢI** hỗ trợ lược đồ xác thực **HTTP Basic** để xác thực các **clients** đã được cấp **client password**.

Ví dụ (có thêm ngắt dòng chỉ để hiển thị):

`Authorization: Basic czZCaGRSa3F0Mzo3RmpmcDBaQnIxS3REUmJuZlZkbUl3`

Ngoài ra, **authorization server CÓ THỂ** hỗ trợ bao gồm **client credentials** trong **request-body** bằng cách sử dụng các tham số sau:

- client_id
    
    REQUIRED. Client identifier được cấp cho client trong quá trình đăng ký được mô tả bởi Phần 2.2.
    
- client_secret
    
    REQUIRED. Client secret. Client CÓ THỂ bỏ qua tham số nếu client secret là một chuỗi rỗng.
    

Việc bao gồm **client credentials** trong **request-body** bằng cách sử dụng hai tham số **KHÔNG ĐƯỢC KHUYẾN NGHỊ** và **NÊN** được giới hạn cho các **clients** không thể trực tiếp sử dụng lược đồ xác thực **HTTP Basic** (hoặc các lược đồ xác thực **HTTP** dựa trên **password** khác). Các tham số chỉ có thể được truyền trong **request-body** và **KHÔNG ĐƯỢC** bao gồm trong **request URI**.

Ví dụ, một yêu cầu để làm mới một **access token** (Phần 6) sử dụng các tham số **body** (có thêm ngắt dòng chỉ để hiển thị):

`POST /token HTTP/1.1
Host: server.example.com
Content-Type: application/x-www-form-urlencoded

grant_type=refresh_token&refresh_token=tGzv3JOkF0XG5Qx2TlKWIA
&client_id=s6BhdRkqt3&client_secret=7Fjfp0ZBr1KtDRbnfVdmIw`

**Authorization server PHẢI** yêu cầu sử dụng **TLS** như mô tả trong Phần 1.6 khi gửi các yêu cầu sử dụng xác thực **password**.

Vì phương thức xác thực **client** này liên quan đến **password**, **authorization server PHẢI** bảo vệ bất kỳ **endpoint** nào sử dụng nó chống lại các cuộc tấn công **brute force**.

#### 2.3.2. Other Authentication Methods

**Authorization server CÓ THỂ** hỗ trợ bất kỳ lược đồ xác thực **HTTP** phù hợp nào đáp ứng yêu cầu bảo mật của nó. Khi sử dụng các phương thức xác thực khác, **authorization server PHẢI** định nghĩa một ánh xạ giữa **client identifier** (bản ghi đăng ký) và lược đồ xác thực.

---

### 2.4. Unregistered Clients

Đặc tả này không loại trừ việc sử dụng các **unregistered clients**. Tuy nhiên, việc sử dụng các **clients** như vậy nằm ngoài phạm vi của đặc tả này và yêu cầu phân tích bảo mật bổ sung và xem xét tác động tương tác của nó.

---

## 3. Protocol Endpoints

Quá trình ủy quyền sử dụng hai **authorization server endpoints** (các tài nguyên **HTTP**):

- **Authorization endpoint** - được **client** sử dụng để có được ủy quyền từ **resource owner** thông qua **user-agent redirection**.
- **Token endpoint** - được **client** sử dụng để đổi một **authorization grant** lấy một **access token**, thường đi kèm với **client authentication**.

Cũng như một **client endpoint**:

- **Redirection endpoint** - được **authorization server** sử dụng để trả về các phản hồi chứa **authorization credentials** cho **client** thông qua **resource owner user-agent**.

Không phải mọi **authorization grant type** đều sử dụng cả hai **endpoints**. Các **extension grant types CÓ THỂ** định nghĩa các **endpoints** bổ sung nếu cần.

---

### 3.1. Authorization Endpoint

**Authorization endpoint** được sử dụng để tương tác với **resource owner** và có được một **authorization grant**. **Authorization server PHẢI** xác minh danh tính của **resource owner** trước tiên. Cách mà **authorization server** xác thực **resource owner** (ví dụ: đăng nhập bằng username và password, **session cookies**) nằm ngoài phạm vi của đặc tả này.

Các phương tiện mà **client** có được vị trí của **authorization endpoint** nằm ngoài phạm vi của đặc tả này, nhưng vị trí này thường được cung cấp trong tài liệu dịch vụ.

**URI endpoint CÓ THỂ** bao gồm một thành phần **query** được định dạng "**application/x-www-form-urlencoded**" (theo Phụ lục B) ([RFC3986] Phần 3.4), thành phần này **PHẢI** được giữ lại khi thêm các tham số **query** bổ sung. **URI endpoint KHÔNG ĐƯỢC** bao gồm một thành phần **fragment**.

Vì các yêu cầu đến **authorization endpoint** dẫn đến việc xác thực người dùng và việc truyền các **clear-text credentials** (trong phản hồi **HTTP**), **authorization server PHẢI** yêu cầu sử dụng **TLS** như mô tả trong Phần 1.6 khi gửi các yêu cầu đến **authorization endpoint**.

**Authorization server PHẢI** hỗ trợ việc sử dụng phương thức **HTTP "GET"** [RFC2616] cho **authorization endpoint** và **CÓ THỂ** cũng hỗ trợ việc sử dụng phương thức "**POST**".

Các tham số được gửi mà không có giá trị **PHẢI** được xử lý như thể chúng bị bỏ qua khỏi yêu cầu. **Authorization server PHẢI** bỏ qua các tham số yêu cầu không được nhận dạng. Các tham số yêu cầu và phản hồi **KHÔNG ĐƯỢC** được bao gồm nhiều hơn một lần.

#### 3.1.1. Response Type

**Authorization endpoint** được sử dụng bởi các luồng **authorization code grant type** và **implicit grant type**. **Client** thông báo cho **authorization server** về **grant type** mong muốn bằng cách sử dụng tham số sau:

- response_type
    
    REQUIRED. Giá trị PHẢI là một trong các giá trị "code" để yêu cầu một authorization code như mô tả trong Phần 4.1.1, "token" để yêu cầu một access token (implicit grant) như mô tả trong Phần 4.2.1, hoặc một giá trị mở rộng đã đăng ký như mô tả trong Phần 8.4.
    

Các **extension response types CÓ THỂ** chứa một danh sách các giá trị được phân tách bằng dấu cách (%x20), trong đó thứ tự của các giá trị không quan trọng (ví dụ: **response type** "a b" giống như "b a"). Ý nghĩa của các **composite response types** như vậy được định nghĩa bởi các đặc tả tương ứng của chúng.

Nếu một **authorization request** thiếu tham số "**response_type**", hoặc nếu **response type** không được hiểu, **authorization server PHẢI** trả về một **error response** như mô tả trong Phần 4.1.2.1.

#### 3.1.2. Redirection Endpoint

Sau khi hoàn thành tương tác với **resource owner**, **authorization server** điều hướng **user-agent** của **resource owner** trở lại **client**. **Authorization server** chuyển hướng **user-agent** đến **redirection endpoint** của **client** đã được thiết lập trước đó với **authorization server** trong quá trình đăng ký **client** hoặc khi thực hiện **authorization request**.

**URI redirection endpoint PHẢI** là một **absolute URI** như được định nghĩa bởi [RFC3986] Phần 4.3. **URI endpoint CÓ THỂ** bao gồm một thành phần **query** được định dạng "**application/x-www-form-urlencoded**" (theo Phụ lục B) ([RFC3986] Phần 3.4), thành phần này **PHẢI** được giữ lại khi thêm các tham số **query** bổ sung. **URI endpoint KHÔNG ĐƯỢC** bao gồm một thành phần **fragment**.

##### 3.1.2.1. Endpoint Request Confidentiality

**Redirection endpoint NÊN** yêu cầu sử dụng **TLS** như mô tả trong Phần 1.6 khi **requested response type** là "**code**" hoặc "**token**", hoặc khi **redirection request** sẽ dẫn đến việc truyền các **sensitive credentials** qua một **open network**. Đặc tả này không bắt buộc sử dụng **TLS** vì tại thời điểm viết bài này, việc yêu cầu các **clients** triển khai **TLS** là một rào cản đáng kể đối với nhiều **client developers**. Nếu **TLS** không khả dụng, **authorization server NÊN** cảnh báo **resource owner** về **insecure endpoint** trước khi chuyển hướng (ví dụ: hiển thị một thông báo trong quá trình **authorization request**).

Thiếu bảo mật lớp vận chuyển có thể có tác động nghiêm trọng đến bảo mật của **client** và các **protected resources** mà nó được ủy quyền truy cập. Việc sử dụng bảo mật lớp vận chuyển đặc biệt quan trọng khi quá trình ủy quyền được sử dụng như một hình thức xác thực **end-user** được ủy quyền bởi **client** (ví dụ: dịch vụ đăng nhập của bên thứ ba).

##### 3.1.2.2. Registration Requirements

**Authorization server PHẢI** yêu cầu các **clients** sau đăng ký **redirection endpoint** của chúng:

- Các **Public clients**.
- Các **Confidential clients** sử dụng **implicit grant type**.

**Authorization server NÊN** yêu cầu tất cả các **clients** đăng ký **redirection endpoint** của chúng trước khi sử dụng **authorization endpoint**.

**Authorization server NÊN** yêu cầu **client** cung cấp **complete redirection URI** (**client CÓ THỂ** sử dụng tham số yêu cầu "**state**" để đạt được tùy chỉnh theo mỗi yêu cầu). Nếu việc yêu cầu đăng ký **complete redirection URI** là không thể, **authorization server NÊN** yêu cầu đăng ký **URI scheme**, **authority**, và **path** (cho phép **client** thay đổi động chỉ thành phần **query** của **redirection URI** khi yêu cầu ủy quyền).

**Authorization server CÓ THỂ** cho phép **client** đăng ký nhiều **redirection endpoints**.

Thiếu yêu cầu đăng ký **redirection URI** có thể cho phép kẻ tấn công sử dụng **authorization endpoint** làm **open redirector** như mô tả trong Phần 10.15.

##### 3.1.2.3. Dynamic Configuration

Nếu nhiều **redirection URIs** đã được đăng ký, nếu chỉ một phần của **redirection URI** đã được đăng ký, hoặc nếu không có **redirection URI** nào được đăng ký, **client PHẢI** bao gồm một **redirection URI** với **authorization request** bằng cách sử dụng tham số yêu cầu "**redirect_uri**".

Khi một **redirection URI** được bao gồm trong một **authorization request**, **authorization server PHẢI** so sánh và khớp giá trị nhận được với ít nhất một trong các **redirection URIs** đã đăng ký (hoặc các thành phần **URI**) như được định nghĩa trong [RFC3986] Phần 6, nếu có bất kỳ **redirection URIs** nào được đăng ký. Nếu đăng ký **client** bao gồm **full redirection URI**, **authorization server PHẢI** so sánh hai **URIs** bằng cách so sánh chuỗi đơn giản như được định nghĩa trong [RFC3986] Phần 6.2.1.

##### 3.1.2.4. Invalid Endpoint

Nếu một **authorization request** không hợp lệ do thiếu, không hợp lệ, hoặc **redirection URI** không khớp, **authorization server NÊN** thông báo cho **resource owner** về lỗi và **KHÔNG ĐƯỢC** tự động chuyển hướng **user-agent** đến **invalid redirection URI**.

##### 3.1.2.5. Endpoint Content

Yêu cầu chuyển hướng đến **endpoint** của **client** thường dẫn đến một phản hồi tài liệu **HTML**, được xử lý bởi **user-agent**. Nếu phản hồi **HTML** được phục vụ trực tiếp là kết quả của yêu cầu chuyển hướng, bất kỳ **script** nào được bao gồm trong tài liệu **HTML** sẽ thực thi với quyền truy cập đầy đủ vào **redirection URI** và các **credentials** mà nó chứa.

**Client KHÔNG NÊN** bao gồm bất kỳ **third-party scripts** nào (ví dụ: **third-party analytics**, **social plug-ins**, **ad networks**) trong phản hồi **redirection endpoint**. Thay vào đó, nó **NÊN** trích xuất **credentials** từ **URI** và chuyển hướng **user-agent** lại đến một **endpoint** khác mà không làm lộ **credentials** (trong **URI** hoặc ở nơi khác). Nếu các **third-party scripts** được bao gồm, **client PHẢI** đảm bảo rằng các **script** của chính nó (được sử dụng để trích xuất và loại bỏ **credentials** khỏi **URI**) sẽ thực thi trước.

---

### 3.2. Token Endpoint

**Token endpoint** được **client** sử dụng để có được một **access token** bằng cách trình bày **authorization grant** hoặc **refresh token** của nó. **Token endpoint** được sử dụng với mọi **authorization grant** ngoại trừ **implicit grant type** (vì **access token** được cấp trực tiếp).

Các phương tiện mà **client** có được vị trí của **token endpoint** nằm ngoài phạm vi của đặc tả này, nhưng vị trí này thường được cung cấp trong tài liệu dịch vụ.

**URI endpoint CÓ THỂ** bao gồm một thành phần **query** được định dạng "**application/x-www-form-urlencoded**" (theo Phụ lục B) ([RFC3986] Phần 3.4), thành phần này **PHẢI** được giữ lại khi thêm các tham số **query** bổ sung. **URI endpoint KHÔNG ĐƯỢC** bao gồm một thành phần **fragment**.

Vì các yêu cầu đến **token endpoint** dẫn đến việc truyền các **clear-text credentials** (trong **HTTP request** và **response**), **authorization server PHẢI** yêu cầu sử dụng **TLS** như mô tả trong Phần 1.6 khi gửi các yêu cầu đến **token endpoint**.

**Client PHẢI** sử dụng phương thức **HTTP "POST"** khi thực hiện các yêu cầu **access token**.

Các tham số được gửi mà không có giá trị **PHẢI** được xử lý như thể chúng bị bỏ qua khỏi yêu cầu. **Authorization server PHẢI** bỏ qua các tham số yêu cầu không được nhận dạng. Các tham số yêu cầu và phản hồi **KHÔNG ĐƯỢC** được bao gồm nhiều hơn một lần.

#### 3.2.1. Client Authentication

Các **confidential clients** hoặc các **clients** khác được cấp **client credentials PHẢI** xác thực với **authorization server** như mô tả trong Phần 2.3 khi thực hiện các yêu cầu đến **token endpoint**. Xác thực **client** được sử dụng cho:

- Thực thi việc ràng buộc **refresh tokens** và **authorization codes** với **client** mà chúng được cấp. Xác thực **client** rất quan trọng khi một **authorization code** được truyền đến **redirection endpoint** qua một kênh không an toàn hoặc khi **redirection URI** chưa được đăng ký đầy đủ.
- Khôi phục từ một **compromised client** bằng cách vô hiệu hóa **client** hoặc thay đổi **credentials** của nó, do đó ngăn chặn kẻ tấn công lạm dụng các **stolen refresh tokens**. Thay đổi một bộ **client credentials** duy nhất nhanh hơn đáng kể so với việc thu hồi toàn bộ các **refresh tokens**.
- Triển khai các phương pháp hay nhất về quản lý xác thực, yêu cầu luân chuyển **credential** định kỳ. Luân chuyển toàn bộ các **refresh tokens** có thể khó khăn, trong khi luân chuyển một bộ **client credentials** duy nhất dễ dàng hơn đáng kể.

Một **client CÓ THỂ** sử dụng tham số yêu cầu "**client_id**" để tự nhận dạng khi gửi các yêu cầu đến **token endpoint**. Trong yêu cầu "**authorization_code**" "**grant_type**" đến **token endpoint**, một **unauthenticated client PHẢI** gửi "**client_id**" của nó để ngăn bản thân vô tình chấp nhận một **code** dành cho một **client** có "**client_id**" khác. Điều này bảo vệ **client** khỏi việc thay thế **authentication code**. (Nó không cung cấp thêm bảo mật cho **protected resource**.)

---

### 3.3. Access Token Scope

Các **authorization** và **token endpoints** cho phép **client** chỉ định **scope** của yêu cầu truy cập bằng cách sử dụng tham số yêu cầu "**scope**". Đổi lại, **authorization server** sử dụng tham số phản hồi "**scope**" để thông báo cho **client** về **scope** của **access token** được cấp.

Giá trị của tham số **scope** được thể hiện dưới dạng một danh sách các chuỗi phân tách bằng dấu cách, có phân biệt chữ hoa, chữ thường. Các chuỗi được định nghĩa bởi **authorization server**. Nếu giá trị chứa nhiều chuỗi phân tách bằng dấu cách, thứ tự của chúng không quan trọng và mỗi chuỗi thêm một phạm vi truy cập bổ sung vào **scope** được yêu cầu.

`scope       = scope-token *( SP scope-token )
scope-token = 1*( %x21 / %x23-5B / %x5D-7E )`

**Authorization server CÓ THỂ** bỏ qua hoàn toàn hoặc một phần **scope** được **client** yêu cầu, dựa trên chính sách của **authorization server** hoặc hướng dẫn của **resource owner**. Nếu **scope** của **access token** được cấp khác với **scope** được **client** yêu cầu, **authorization server PHẢI** bao gồm tham số phản hồi "**scope**" để thông báo cho **client** về **scope** thực tế được cấp.

Nếu **client** bỏ qua tham số **scope** khi yêu cầu ủy quyền, **authorization server PHẢI** xử lý yêu cầu bằng cách sử dụng một giá trị mặc định được định nghĩa trước hoặc làm cho yêu cầu thất bại và cho biết một **invalid scope**. **Authorization server NÊN** ghi lại các yêu cầu về **scope** và giá trị mặc định của nó (nếu được định nghĩa).

---

## 4. Obtaining Authorization

Để yêu cầu một **access token**, **client** phải có được ủy quyền từ **resource owner**. Việc ủy quyền được thể hiện dưới dạng một **authorization grant**, mà **client** sử dụng để yêu cầu **access token**. OAuth định nghĩa bốn **grant types**: **authorization code**, **implicit**, **resource owner password credentials**, và **client credentials**. Nó cũng cung cấp một cơ chế mở rộng để định nghĩa các **grant types** bổ sung.

---

### 4.1. Authorization Code Grant

**Authorization code grant type** được sử dụng để có được cả **access tokens** và **refresh tokens** và được tối ưu hóa cho các **confidential clients**. Vì đây là một luồng dựa trên **redirection**, **client** phải có khả năng tương tác với **user-agent** của **resource owner** (thường là một **web browser**) và có khả năng nhận các yêu cầu đến (thông qua **redirection**) từ **authorization server**.

     `+----------+
     | Resource |
     |   Owner  |
     |          |
     +----------+
          ^
          |
         (B)
     +----|-----+          Client Identifier      +---------------+
     |         -+----(A)-- & Redirection URI ---->|               |
     |  User-   |                                 | Authorization |
     |  Agent  -+----(B)-- User authenticates --->|     Server    |
     |          |                                 |               |
     |         -+----(C)-- Authorization Code ---<|               |
     +-|----|---+                                 +---------------+
       |    |                                         ^      v
      (A)  (C)                                        |      |
       |    |                                         |      |
       ^    v                                         |      |
     +---------+                                      |      |
     |         |>---(D)-- Authorization Code ---------'      |
     |  Client |          & Redirection URI                  |
     |         |                                             |
     |         |<---(E)----- Access Token -------------------'
     +---------+       (w/ Optional Refresh Token)

   Note: The lines illustrating steps (A), (B), and (C) are broken into
   two parts as they pass through the user-agent.

                     Figure 3: Authorization Code Flow`

Luồng minh họa trong Hình 3 bao gồm các bước sau:

(A) **Client** khởi tạo luồng bằng cách điều hướng **user-agent** của **resource owner** đến **authorization endpoint**. **Client** bao gồm **client identifier**, **requested scope**, **local state** và **redirection URI** mà **authorization server** sẽ gửi **user-agent** trở lại khi quyền truy cập được cấp (hoặc từ chối).

(B) **Authorization server** xác thực **resource owner** (thông qua **user-agent**) và xác định liệu **resource owner** cấp hay từ chối yêu cầu truy cập của **client**.

(C) Giả sử **resource owner** cấp quyền truy cập, **authorization server** chuyển hướng **user-agent** trở lại **client** bằng cách sử dụng **redirection URI** được cung cấp trước đó (trong yêu cầu hoặc trong quá trình đăng ký **client**). **Redirection URI** bao gồm một **authorization code** và bất kỳ **local state** nào được **client** cung cấp trước đó.

(D) **Client** yêu cầu một **access token** từ **token endpoint** của **authorization server** bằng cách bao gồm **authorization code** nhận được ở bước trước. Khi thực hiện yêu cầu, **client** xác thực với **authorization server**. **Client** bao gồm **redirection URI** được sử dụng để lấy **authorization code** để xác minh.

(E) **Authorization server** xác thực **client**, xác nhận **authorization code** và đảm bảo rằng **redirection URI** nhận được khớp với **URI** được sử dụng để chuyển hướng **client** ở bước (C). Nếu hợp lệ, **authorization server** phản hồi lại bằng một **access token** và, tùy chọn, một **refresh token**.

#### 4.1.1. Authorization Request

**Client** xây dựng **request URI** bằng cách thêm các tham số sau vào thành phần **query** của **authorization endpoint URI** bằng cách sử dụng định dạng "**application/x-www-form-urlencoded**", theo Phụ lục B:

- response_type
    
    REQUIRED. Giá trị PHẢI được đặt thành "code".
    
- client_id
    
    REQUIRED. Client identifier như mô tả trong Phần 2.2.
    
- redirect_uri
    
    OPTIONAL. Như mô tả trong Phần 3.1.2.
    
- scope
    
    OPTIONAL. Scope của yêu cầu truy cập như mô tả trong Phần 3.3.
    
- state
    
    RECOMMENDED. Một giá trị opaque được client sử dụng để duy trì state giữa yêu cầu và callback. Authorization server bao gồm giá trị này khi chuyển hướng user-agent trở lại client. Tham số NÊN được sử dụng để ngăn chặn cross-site request forgery như mô tả trong Phần 10.12.
    

**Client** điều hướng **resource owner** đến **URI** đã xây dựng bằng cách sử dụng một phản hồi **HTTP redirection**, hoặc bằng các phương tiện khác có sẵn cho nó thông qua **user-agent**.

Ví dụ, **client** điều hướng **user-agent** để thực hiện yêu cầu **HTTP** sau bằng **TLS** (có thêm ngắt dòng chỉ để hiển thị):

`GET /authorize?response_type=code&client_id=s6BhdRkqt3&state=xyz
    &redirect_uri=https%3A%2F%2Fclient%2Eexample%2Ecom%2Fcb HTTP/1.1
Host: server.example.com`

**Authorization server** xác nhận yêu cầu để đảm bảo rằng tất cả các tham số bắt buộc đều có mặt và hợp lệ. Nếu yêu cầu hợp lệ, **authorization server** xác thực **resource owner** và có được quyết định ủy quyền (bằng cách hỏi **resource owner** hoặc bằng cách thiết lập phê duyệt thông qua các phương tiện khác).

Khi một quyết định được thiết lập, **authorization server** điều hướng **user-agent** đến **client redirection URI** được cung cấp bằng cách sử dụng một phản hồi **HTTP redirection**, hoặc bằng các phương tiện khác có sẵn cho nó thông qua **user-agent**.

#### 4.1.2. Authorization Response

Nếu **resource owner** cấp yêu cầu truy cập, **authorization server** cấp một **authorization code** và gửi nó cho **client** bằng cách thêm các tham số sau vào thành phần **query** của **redirection URI** bằng cách sử dụng định dạng "**application/x-www-form-urlencoded**", theo Phụ lục B:

- code
    
    REQUIRED. Authorization code được tạo bởi authorization server. Authorization code PHẢI hết hạn ngay sau khi nó được cấp để giảm thiểu rủi ro rò rỉ. Thời gian tồn tại tối đa của authorization code là 10 phút được KHUYẾN NGHỊ. Client KHÔNG ĐƯỢC sử dụng authorization code nhiều hơn một lần. Nếu một authorization code được sử dụng nhiều hơn một lần, authorization server PHẢI từ chối yêu cầu và NÊN thu hồi (khi có thể) tất cả các tokens đã được cấp trước đó dựa trên authorization code đó. Authorization code được gắn với client identifier và redirection URI.
    
- state
    
    REQUIRED nếu tham số "state" có mặt trong client authorization request. Giá trị chính xác nhận được từ client.
    

Ví dụ, **authorization server** chuyển hướng **user-agent** bằng cách gửi phản hồi **HTTP** sau:

`HTTP/1.1 302 Found
Location: https://client.example.com/cb?code=SplxlOBeZQQYbYS6WxSbIA
          &state=xyz`

**Client PHẢI** bỏ qua các tham số phản hồi không được nhận dạng. Kích thước chuỗi **authorization code** không được định nghĩa bởi đặc tả này. **Client** nên tránh đưa ra các giả định về kích thước giá trị **code**. **Authorization server NÊN** ghi lại kích thước của bất kỳ giá trị nào mà nó cấp.

##### 4.1.2.1. Error Response

Nếu yêu cầu thất bại do **redirection URI** thiếu, không hợp lệ, hoặc không khớp, hoặc nếu **client identifier** thiếu hoặc không hợp lệ, **authorization server NÊN** thông báo cho **resource owner** về lỗi và **KHÔNG ĐƯỢC** tự động chuyển hướng **user-agent** đến **invalid redirection URI**.

Nếu **resource owner** từ chối yêu cầu truy cập hoặc nếu yêu cầu thất bại vì những lý do khác ngoài **redirection URI** thiếu hoặc không hợp lệ, **authorization server** thông báo cho **client** bằng cách thêm các tham số sau vào thành phần **query** của **redirection URI** bằng cách sử dụng định dạng "**application/x-www-form-urlencoded**", theo Phụ lục B:

- error
    
    REQUIRED. Một error code ASCII [USASCII] duy nhất từ các loại sau:
    
    - invalid_request
        
        Yêu cầu thiếu một tham số bắt buộc, bao gồm một giá trị tham số không hợp lệ, bao gồm một tham số nhiều hơn một lần, hoặc bị định dạng sai.
        
    - unauthorized_client
        
        Client không được ủy quyền để yêu cầu một authorization code bằng phương pháp này.
        
    - access_denied
        
        Resource owner hoặc authorization server đã từ chối yêu cầu.
        
    - unsupported_response_type
        
        Authorization server không hỗ trợ việc có được một authorization code bằng phương pháp này.
        
    - invalid_scope
        
        Requested scope không hợp lệ, không xác định, hoặc bị định dạng sai.
        
    - server_error
        
        Authorization server gặp phải một điều kiện không mong muốn đã ngăn nó thực hiện yêu cầu. (Mã lỗi này là cần thiết vì mã trạng thái HTTP 500 Internal Server Error không thể được trả về client thông qua HTTP redirect.)
        
    - temporarily_unavailable
        
        Authorization server hiện không thể xử lý yêu cầu do máy chủ bị quá tải tạm thời hoặc đang bảo trì. (Mã lỗi này là cần thiết vì mã trạng thái HTTP 503 Service Unavailable không thể được trả về client thông qua HTTP redirect.)
        
    
    Các giá trị cho tham số "**error**" **KHÔNG ĐƯỢC** bao gồm các ký tự ngoài tập hợp %x20-21 / %x23-5B / %x5D-7E.
    
- error_description
    
    OPTIONAL. Văn bản ASCII [USASCII] dễ đọc cung cấp thông tin bổ sung, được sử dụng để hỗ trợ client developer trong việc hiểu lỗi đã xảy ra. Các giá trị cho tham số "error_description" KHÔNG ĐƯỢC bao gồm các ký tự ngoài tập hợp %x20-21 / %x23-5B / %x5D-7E.
    
- error_uri
    
    OPTIONAL. Một URI xác định một trang web dễ đọc với thông tin về lỗi, được sử dụng để cung cấp cho client developer thông tin bổ sung về lỗi. Các giá trị cho tham số "error_uri" PHẢI tuân thủ cú pháp URI-reference và do đó KHÔNG ĐƯỢC bao gồm các ký tự ngoài tập hợp %x21 / %x23-5B / %x5D-7E.
    
- state
    
    REQUIRED nếu tham số "state" có mặt trong client authorization request. Giá trị chính xác nhận được từ client.
    

Ví dụ, **authorization server** chuyển hướng **user-agent** bằng cách gửi phản hồi **HTTP** sau:

`HTTP/1.1 302 Found
Location: https://client.example.com/cb?error=access_denied&state=xyz`

#### 4.1.3. Access Token Request

**Client** thực hiện một yêu cầu đến **token endpoint** bằng cách gửi các tham số sau bằng định dạng "**application/x-www-form-urlencoded**" theo Phụ lục B với mã hóa ký tự **UTF-8** trong **HTTP request entity-body**:

- grant_type
    
    REQUIRED. Giá trị PHẢI được đặt thành "authorization_code".
    
- code
    
    REQUIRED. Authorization code nhận được từ authorization server.
    
- redirect_uri
    
    REQUIRED, nếu tham số "redirect_uri" được bao gồm trong authorization request như mô tả trong Phần 4.1.1, và các giá trị của chúng PHẢI giống hệt nhau.
    
- client_id
    
    REQUIRED, nếu client không xác thực với authorization server như mô tả trong Phần 3.2.1.
    

Nếu **client type** là **confidential** hoặc **client** được cấp **client credentials** (hoặc được gán các yêu cầu xác thực khác), **client PHẢI** xác thực với **authorization server** như mô tả trong Phần 3.2.1.

Ví dụ, **client** thực hiện yêu cầu **HTTP** sau bằng **TLS** (có thêm ngắt dòng chỉ để hiển thị):

`POST /token HTTP/1.1
Host: server.example.com
Authorization: Basic czZCaGRSa3F0MzpnWDFmQmF0M2JW
Content-Type: application/x-www-form-urlencoded

grant_type=authorization_code&code=SplxlOBeZQQYbYS6WxSbIA
&redirect_uri=https%3A%2F%2Fclient%2Eexample%2Ecom%2Fcb`

**Authorization server PHẢI**:

- yêu cầu xác thực **client** cho các **confidential clients** hoặc cho bất kỳ **client** nào đã được cấp **client credentials** (hoặc với các yêu cầu xác thực khác),
- xác thực **client** nếu xác thực **client** được bao gồm,
- đảm bảo rằng **authorization code** đã được cấp cho **confidential client** đã xác thực, hoặc nếu **client** là **public**, đảm bảo rằng **code** đã được cấp cho "**client_id**" trong yêu cầu,
- xác minh rằng **authorization code** hợp lệ, và
- đảm bảo rằng tham số "**redirect_uri**" có mặt nếu tham số "**redirect_uri**" được bao gồm trong **initial authorization request** như mô tả trong Phần 4.1.1, và nếu được bao gồm, đảm bảo rằng các giá trị của chúng giống hệt nhau.

#### 4.1.4. Access Token Response

Nếu yêu cầu **access token** hợp lệ và được ủy quyền, **authorization server** cấp một **access token** và **refresh token** tùy chọn như mô tả trong Phần 5.1. Nếu xác thực **client** của yêu cầu thất bại hoặc không hợp lệ, **authorization server** trả về một **error response** như mô tả trong Phần 5.2.

Một ví dụ về phản hồi thành công:

JSON

# 

`HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8
Cache-Control: no-store
Pragma: no-cache

{
  "access_token":"2YotnFZFEjr1zCsicMWpAA",
  "token_type":"example",
  "expires_in":3600,
  "refresh_token":"tGzv3JOkF0XG5Qx2TlKWIA",
  "example_parameter":"example_value"
}`

---

### 4.2. Implicit Grant

**Implicit grant type** được sử dụng để có được **access tokens** (nó không hỗ trợ việc cấp **refresh tokens**) và được tối ưu hóa cho các **public clients** được biết là vận hành một **redirection URI** cụ thể. Các **clients** này thường được triển khai trong một **browser** bằng cách sử dụng một ngôn ngữ **scripting** như **JavaScript**.

Vì đây là một luồng dựa trên **redirection**, **client** phải có khả năng tương tác với **user-agent** của **resource owner** (thường là một **web browser**) và có khả năng nhận các yêu cầu đến (thông qua **redirection**) từ **authorization server**.

Không giống như **authorization code grant type**, trong đó **client** thực hiện các yêu cầu riêng biệt để ủy quyền và lấy **access token**, **client** nhận **access token** là kết quả của **authorization request**.

**Implicit grant type** không bao gồm **client authentication**, và dựa vào sự hiện diện của **resource owner** và việc đăng ký của **redirection URI**. Bởi vì **access token** được mã hóa vào **redirection URI**, nó có thể bị lộ cho **resource owner** và các ứng dụng khác nằm trên cùng thiết bị.

     `+----------+
     | Resource |
     |  Owner   |
     |          |
     +----------+
          ^
          |
         (B)
     +----|-----+          Client Identifier     +---------------+
     |         -+----(A)-- & Redirection URI --->|               |
     |  User-   |                                | Authorization |
     |  Agent  -|----(B)-- User authenticates -->|     Server    |
     |          |                                |               |
     |          |<---(C)--- Redirection URI ----<|               |
     |          |          with Access Token     +---------------+
     |          |            in Fragment
     |          |                                +---------------+
     |          |----(D)--- Redirection URI ---->|   Web-Hosted  |
     |          |          without Fragment      |     Client    |
     |          |                                |    Resource   |
     |     (F)  |<---(E)------- Script ---------<|               |
     |          |                                +---------------+
     +-|--------+
       |    |
      (A)  (G) Access Token
       |    |
       ^    v
     +---------+
     |         |
     |  Client |
     |         |
     +---------+

   Note: The lines illustrating steps (A) and (B) are broken into two
   parts as they pass through the user-agent.

                       Figure 4: Implicit Grant Flow`

Luồng minh họa trong Hình 4 bao gồm các bước sau:

(A) **Client** khởi tạo luồng bằng cách điều hướng **user-agent** của **resource owner** đến **authorization endpoint**. **Client** bao gồm **client identifier**, **requested scope**, **local state** và **redirection URI** mà **authorization server** sẽ gửi **user-agent** trở lại khi quyền truy cập được cấp (hoặc từ chối).

(B) **Authorization server** xác thực **resource owner** (thông qua **user-agent**) và xác định liệu **resource owner** cấp hay từ chối yêu cầu truy cập của **client**.

(C) Giả sử **resource owner** cấp quyền truy cập, **authorization server** chuyển hướng **user-agent** trở lại **client** bằng cách sử dụng **redirection URI** được cung cấp trước đó. **Redirection URI** bao gồm **access token** trong **URI fragment**.

(D) **User-agent** tuân theo các hướng dẫn chuyển hướng bằng cách thực hiện một yêu cầu đến **web-hosted client resource** (không bao gồm **fragment** theo [RFC2616]). **User-agent** giữ lại thông tin **fragment** cục bộ.

(E) **Web-hosted client resource** trả về một trang web (thường là một tài liệu **HTML** với một **script** nhúng) có khả năng truy cập **full redirection URI** bao gồm **fragment** được giữ lại bởi **user-agent**, và trích xuất **access token** (và các tham số khác) chứa trong **fragment**.

(F) **User-agent** thực thi **script** được cung cấp bởi **web-hosted client resource** cục bộ, **script** này trích xuất **access token**.

(G) **User-agent** chuyển **access token** cho **client**.

Xem Phần 1.3.2 và 9 để biết thông tin cơ bản về việc sử dụng **implicit grant**. Xem Phần 10.3 và 10.16 để biết các cân nhắc bảo mật quan trọng khi sử dụng **implicit grant**.

#### 4.2.1. Authorization Request

**Client** xây dựng **request URI** bằng cách thêm các tham số sau vào thành phần **query** của **authorization endpoint URI** bằng cách sử dụng định dạng "**application/x-www-form-urlencoded**", theo Phụ lục B:

- response_type
    
    REQUIRED. Giá trị PHẢI được đặt thành "token".
    
- client_id
    
    REQUIRED. Client identifier như mô tả trong Phần 2.2.
    
- redirect_uri
    
    OPTIONAL. Như mô tả trong Phần 3.1.2.
    
- scope
    
    OPTIONAL. Scope của yêu cầu truy cập như mô tả trong Phần 3.3.
    
- state
    
    RECOMMENDED. Một giá trị opaque được client sử dụng để duy trì state giữa yêu cầu và callback. Authorization server bao gồm giá trị này khi chuyển hướng user-agent trở lại client. Tham số NÊN được sử dụng để ngăn chặn cross-site request forgery như mô tả trong Phần 10.12.
    

**Client** điều hướng **resource owner** đến **URI** đã xây dựng bằng cách sử dụng một phản hồi **HTTP redirection**, hoặc bằng các phương tiện khác có sẵn cho nó thông qua **user-agent**.

Ví dụ, **client** điều hướng **user-agent** để thực hiện yêu cầu **HTTP** sau bằng **TLS** (có thêm ngắt dòng chỉ để hiển thị):

`GET /authorize?response_type=token&client_id=s6BhdRkqt3&state=xyz
    &redirect_uri=https%3A%2F%2Fclient%2Eexample%2Ecom%2Fcb HTTP/1.1
Host: server.example.com`

**Authorization server** xác nhận yêu cầu để đảm bảo rằng tất cả các tham số bắt buộc đều có mặt và hợp lệ. **Authorization server PHẢI** xác minh rằng **redirection URI** mà nó sẽ chuyển hướng **access token** đến khớp với một **redirection URI** đã được **client** đăng ký như mô tả trong Phần 3.1.2.

Nếu yêu cầu hợp lệ, **authorization server** xác thực **resource owner** và có được quyết định ủy quyền (bằng cách hỏi **resource owner** hoặc bằng cách thiết lập phê duyệt thông qua các phương tiện khác).

Khi một quyết định được thiết lập, **authorization server** điều hướng **user-agent** đến **client redirection URI** được cung cấp bằng cách sử dụng một phản hồi **HTTP redirection**, hoặc bằng các phương tiện khác có sẵn cho nó thông qua **user-agent**.

#### 4.2.2. Access Token Response

Nếu **resource owner** cấp yêu cầu truy cập, **authorization server** cấp một **access token** và gửi nó cho **client** bằng cách thêm các tham số sau vào thành phần **fragment** của **redirection URI** bằng cách sử dụng định dạng "**application/x-www-form-urlencoded**", theo Phụ lục B:

- access_token
    
    REQUIRED. Access token được cấp bởi authorization server.
    
- token_type
    
    REQUIRED. Loại token được cấp như mô tả trong Phần 7.1. Giá trị không phân biệt chữ hoa, chữ thường.
    
- expires_in
    
    RECOMMENDED. Thời gian tồn tại tính bằng giây của access token. Ví dụ, giá trị "3600" biểu thị rằng access token sẽ hết hạn trong một giờ kể từ thời điểm phản hồi được tạo. Nếu bị bỏ qua, authorization server NÊN cung cấp thời gian hết hạn bằng các phương tiện khác hoặc ghi lại giá trị mặc định.
    
- scope
    
    OPTIONAL, nếu giống hệt với scope được client yêu cầu; nếu không, REQUIRED. Scope của access token như mô tả trong Phần 3.3.
    
- state
    
    REQUIRED nếu tham số "state" có mặt trong client authorization request. Giá trị chính xác nhận được từ client.
    

**Authorization server KHÔNG ĐƯỢC** cấp một **refresh token**.

Ví dụ, **authorization server** chuyển hướng **user-agent** bằng cách gửi phản hồi **HTTP** sau (có thêm ngắt dòng chỉ để hiển thị):

`HTTP/1.1 302 Found
Location: http://example.com/cb#access_token=2YotnFZFEjr1zCsicMWpAA
          &state=xyz&token_type=example&expires_in=3600`

Các nhà phát triển nên lưu ý rằng một số **user-agents** không hỗ trợ việc bao gồm thành phần **fragment** trong trường tiêu đề phản hồi **HTTP "Location"**. Các **clients** như vậy sẽ yêu cầu sử dụng các phương pháp khác để chuyển hướng **client** ngoài phản hồi chuyển hướng **3xx** -- ví dụ, trả về một trang **HTML** bao gồm một nút 'tiếp tục' với hành động được liên kết với **redirection URI**.

**Client PHẢI** bỏ qua các tham số phản hồi không được nhận dạng. Kích thước chuỗi **access token** không được định nghĩa bởi đặc tả này. **Client** nên tránh đưa ra các giả định về kích thước giá trị. **Authorization server NÊN** ghi lại kích thước của bất kỳ giá trị nào mà nó cấp.

##### 4.2.2.1. Error Response

Nếu yêu cầu thất bại do **redirection URI** thiếu, không hợp lệ, hoặc không khớp, hoặc nếu **client identifier** thiếu hoặc không hợp lệ, **authorization server NÊN** thông báo cho **resource owner** về lỗi và **KHÔNG ĐƯỢC** tự động chuyển hướng **user-agent** đến **invalid redirection URI**.

Nếu **resource owner** từ chối yêu cầu truy cập hoặc nếu yêu cầu thất bại vì những lý do khác ngoài **redirection URI** thiếu hoặc không hợp lệ, **authorization server** thông báo cho **client** bằng cách thêm các tham số sau vào thành phần **fragment** của **redirection URI** bằng cách sử dụng định dạng "**application/x-www-form-urlencoded**", theo Phụ lục B:

- error
    
    REQUIRED. Một error code ASCII [USASCII] duy nhất từ các loại sau:
    
    - invalid_request
        
        Yêu cầu thiếu một tham số bắt buộc, bao gồm một giá trị tham số không hợp lệ, bao gồm một tham số nhiều hơn một lần, hoặc bị định dạng sai.
        
    - unauthorized_client
        
        Client không được ủy quyền để yêu cầu một access token bằng phương pháp này.
        
    - access_denied
        
        Resource owner hoặc authorization server đã từ chối yêu cầu.
        
    - unsupported_response_type
        
        Authorization server không hỗ trợ việc có được một access token bằng phương pháp này.
        
    - invalid_scope
        
        Requested scope không hợp lệ, không xác định, hoặc bị định dạng sai.
        
    - server_error
        
        Authorization server gặp phải một điều kiện không mong muốn đã ngăn nó thực hiện yêu cầu. (Mã lỗi này là cần thiết vì mã trạng thái HTTP 500 Internal Server Error không thể được trả về client thông qua HTTP redirect.)
        
    - temporarily_unavailable
        
        Authorization server hiện không thể xử lý yêu cầu do máy chủ bị quá tải tạm thời hoặc đang bảo trì. (Mã lỗi này là cần thiết vì mã trạng thái HTTP 503 Service Unavailable không thể được trả về client thông qua HTTP redirect.)
        
    
    Các giá trị cho tham số "**error**" **KHÔNG ĐƯỢC** bao gồm các ký tự ngoài tập hợp %x20-21 / %x23-5B / %x5D-7E.
    
- error_description
    
    OPTIONAL. Văn bản ASCII [USASCII] dễ đọc cung cấp thông tin bổ sung, được sử dụng để hỗ trợ client developer trong việc hiểu lỗi đã xảy ra. Các giá trị cho tham số "error_description" KHÔNG ĐƯỢC bao gồm các ký tự ngoài tập hợp %x20-21 / %x23-5B / %x5D-7E.
    
- error_uri
    
    OPTIONAL. Một URI xác định một trang web dễ đọc với thông tin về lỗi, được sử dụng để cung cấp cho client developer thông tin bổ sung về lỗi. Các giá trị cho tham số "error_uri" PHẢI tuân thủ cú pháp URI-reference và do đó KHÔNG ĐƯỢC bao gồm các ký tự ngoài tập hợp %x21 / %x23-5B / %x5D-7E.
    
- state
    
    REQUIRED nếu tham số "state" có mặt trong client authorization request. Giá trị chính xác nhận được từ client.
    

Ví dụ, **authorization server** chuyển hướng **user-agent** bằng cách gửi phản hồi **HTTP** sau:

`HTTP/1.1 302 Found
Location: https://client.example.com/cb#error=access_denied&state=xyz`

---

### 4.3. Resource Owner Password Credentials Grant

**Resource owner password credentials grant type** phù hợp trong các trường hợp **resource owner** có mối quan hệ tin cậy với **client**, chẳng hạn như hệ điều hành thiết bị hoặc một ứng dụng có đặc quyền cao. **Authorization server** nên đặc biệt cẩn trọng khi bật loại **grant** này và chỉ cho phép nó khi các luồng khác không khả thi.

Loại **grant** này phù hợp với các **clients** có khả năng lấy **credentials** của **resource owner** (username và password, thường bằng cách sử dụng một biểu mẫu tương tác). Nó cũng được sử dụng để chuyển đổi các **clients** hiện có sử dụng các lược đồ xác thực trực tiếp như **HTTP Basic** hoặc **Digest authentication** sang OAuth bằng cách chuyển đổi các **credentials** đã lưu trữ thành một **access token**.

     `+----------+
     | Resource |
     |  Owner   |
     |          |
     +----------+
          v
          |    Resource Owner
         (A) Password Credentials
          |
          v
     +---------+                                  +---------------+
     |         |>--(B)---- Resource Owner ------->|               |
     |         |         Password Credentials     | Authorization |
     | Client  |                                  |     Server    |
     |         |<--(C)---- Access Token ---------<|               |
     |         |    (w/ Optional Refresh Token)   |               |
     +---------+                                  +---------------+

            Figure 5: Resource Owner Password Credentials Flow`

Luồng minh họa trong Hình 5 bao gồm các bước sau:

(A) **Resource owner** cung cấp cho **client** username và password của mình.

(B) **Client** yêu cầu một **access token** từ **token endpoint** của **authorization server** bằng cách bao gồm các **credentials** nhận được từ **resource owner**. Khi thực hiện yêu cầu, **client** xác thực với **authorization server**.

(C) **Authorization server** xác thực **client** và xác nhận **resource owner credentials**, và nếu hợp lệ, cấp một **access token**.

#### 4.3.1. Authorization Request and Response

Phương pháp mà **client** có được **resource owner credentials** nằm ngoài phạm vi của đặc tả này. **Client PHẢI** loại bỏ các **credentials** sau khi đã có được một **access token**.

#### 4.3.2. Access Token Request

**Client** thực hiện một yêu cầu đến **token endpoint** bằng cách thêm các tham số sau bằng định dạng "**application/x-www-form-urlencoded**" theo Phụ lục B với mã hóa ký tự **UTF-8** trong **HTTP request entity-body**:

- grant_type
    
    REQUIRED. Giá trị PHẢI được đặt thành "password".
    
- username
    
    REQUIRED. Username của resource owner.
    
- password
    
    REQUIRED. Password của resource owner.
    
- scope
    
    OPTIONAL. Scope của yêu cầu truy cập như mô tả trong Phần 3.3.
    

Nếu **client type** là **confidential** hoặc **client** được cấp **client credentials** (hoặc được gán các yêu cầu xác thực khác), **client PHẢI** xác thực với **authorization server** như mô tả trong Phần 3.2.1.

Ví dụ, **client** thực hiện yêu cầu **HTTP** sau bằng **transport-layer security** (có thêm ngắt dòng chỉ để hiển thị):

`POST /token HTTP/1.1
Host: server.example.com
Authorization: Basic czZCaGRSa3F0MzpnWDFmQmF0M2JW
Content-Type: application/x-www-form-urlencoded

grant_type=password&username=johndoe&password=A3ddj3w`

**Authorization server PHẢI**:

- yêu cầu xác thực **client** cho các **confidential clients** hoặc cho bất kỳ **client** nào đã được cấp **client credentials** (hoặc với các yêu cầu xác thực khác),
- xác thực **client** nếu xác thực **client** được bao gồm, và
- xác nhận **resource owner password credentials** bằng cách sử dụng thuật toán xác nhận password hiện có của nó.

Vì yêu cầu **access token** này sử dụng password của **resource owner**, **authorization server PHẢI** bảo vệ **endpoint** chống lại các cuộc tấn công **brute force** (ví dụ: sử dụng **rate-limitation** hoặc tạo **alerts**).

#### 4.3.3. Access Token Response

Nếu yêu cầu **access token** hợp lệ và được ủy quyền, **authorization server** cấp một **access token** và **refresh token** tùy chọn như mô tả trong Phần 5.1. Nếu xác thực **client** của yêu cầu thất bại hoặc không hợp lệ, **authorization server** trả về một **error response** như mô tả trong Phần 5.2.

Một ví dụ về phản hồi thành công:

JSON

# 

`HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8
Cache-Control: no-store
Pragma: no-cache

{
  "access_token":"2YotnFZFEjr1zCsicMWpAA",
  "token_type":"example",
  "expires_in":3600,
  "refresh_token":"tGzv3JOkF0XG5Qx2TlKWIA",
  "example_parameter":"example_value"
}`

---

### 4.4. Client Credentials Grant

**Client** có thể yêu cầu một **access token** chỉ bằng cách sử dụng **client credentials** của nó (hoặc các phương tiện xác thực được hỗ trợ khác) khi **client** đang yêu cầu quyền truy cập vào các **protected resources** thuộc quyền kiểm soát của nó, hoặc của một **resource owner** khác đã được sắp xếp trước với **authorization server** (phương pháp này nằm ngoài phạm vi của đặc tả này).

**Client credentials grant type CHỈ ĐƯỢC** sử dụng bởi các **confidential clients**.

     `+---------+                                  +---------------+
     |         |                                  |               |
     |         |>--(A)- Client Authentication --->| Authorization |
     | Client  |                                  |     Server    |
     |         |<--(B)---- Access Token ---------<|               |
     |         |                                  |               |
     +---------+                                  +---------------+

                     Figure 6: Client Credentials Flow`

Luồng minh họa trong Hình 6 bao gồm các bước sau:

(A) **Client** xác thực với **authorization server** và yêu cầu một **access token** từ **token endpoint**.

(B) **Authorization server** xác thực **client**, và nếu hợp lệ, cấp một **access token**.

#### 4.4.1. Authorization Request and Response

Vì **client authentication** được sử dụng làm **authorization grant**, không cần yêu cầu ủy quyền bổ sung.

#### 4.4.2. Access Token Request

**Client** thực hiện một yêu cầu đến **token endpoint** bằng cách thêm các tham số sau bằng định dạng "**application/x-www-form-urlencoded**" theo Phụ lục B với mã hóa ký tự **UTF-8** trong **HTTP request entity-body**:

- grant_type
    
    REQUIRED. Giá trị PHẢI được đặt thành "client_credentials".
    
- scope
    
    OPTIONAL. Scope của yêu cầu truy cập như mô tả trong Phần 3.3.
    

**Client PHẢI** xác thực với **authorization server** như mô tả trong Phần 3.2.1.

Ví dụ, **client** thực hiện yêu cầu **HTTP** sau bằng **transport-layer security** (có thêm ngắt dòng chỉ để hiển thị):

`POST /token HTTP/1.1
Host: server.example.com
Authorization: Basic czZCaGRSa3F0MzpnWDFmQmF0M2JW
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials`

**Authorization server PHẢI** xác thực **client**.

#### 4.4.3. Access Token Response

Nếu yêu cầu **access token** hợp lệ và được ủy quyền, **authorization server** cấp một **access token** như mô tả trong Phần 5.1. Một **refresh token KHÔNG NÊN** được bao gồm. Nếu xác thực **client** của yêu cầu thất bại hoặc không hợp lệ, **authorization server** trả về một **error response** như mô tả trong Phần 5.2.

Một ví dụ về phản hồi thành công:

JSON

# 

`HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8
Cache-Control: no-store
Pragma: no-cache

{
  "access_token":"2YotnFZFEjr1zCsicMWpAA",
  "token_type":"example",
  "expires_in":3600,
  "example_parameter":"example_value"
}`

---

### 4.5. Extension Grants

**Client** sử dụng một **extension grant type** bằng cách chỉ định **grant type** bằng cách sử dụng một **absolute URI** (được định nghĩa bởi **authorization server**) làm giá trị của tham số "**grant_type**" của **token endpoint**, và bằng cách thêm bất kỳ tham số bổ sung nào cần thiết.

Ví dụ, để yêu cầu một **access token** bằng cách sử dụng **Security Assertion Markup Language (SAML) 2.0 assertion grant type** như được định nghĩa bởi [OAuth-SAML2], **client** có thể thực hiện yêu cầu **HTTP** sau bằng **TLS** (có thêm ngắt dòng chỉ để hiển thị):

`POST /token HTTP/1.1
Host: server.example.com
Content-Type: application/x-www-form-urlencoded

grant_type=urn%3Aietf%3Aparams%3Aoauth%3Agrant-type%3Asaml2-
bearer&assertion=PEFzc2VydGlvbiBJc3N1ZUluc3RhbnQ9IjIwMTEtMDU
[...omitted for brevity...]aG5TdGF0ZW1lbnQ-PC9Bc3NlcnRpb24-`

Nếu yêu cầu **access token** hợp lệ và được ủy quyền, **authorization server** cấp một **access token** và **refresh token** tùy chọn như mô tả trong Phần 5.1. Nếu xác thực **client** của yêu cầu thất bại hoặc không hợp lệ, **authorization server** trả về một **error response** như mô tả trong Phần 5.2.

---

## 5. Issuing an Access Token

Nếu yêu cầu **access token** hợp lệ và được ủy quyền, **authorization server** cấp một **access token** và **refresh token** tùy chọn như mô tả trong Phần 5.1. Nếu yêu cầu xác thực **client** thất bại hoặc không hợp lệ, **authorization server** trả về một **error response** như mô tả trong Phần 5.2.

---

### 5.1. Successful Response

**Authorization server** cấp một **access token** và **refresh token** tùy chọn, và xây dựng phản hồi bằng cách thêm các tham số sau vào **entity-body** của phản hồi **HTTP** với mã trạng thái **200 (OK)**:

- access_token
    
    REQUIRED. Access token được cấp bởi authorization server.
    
- token_type
    
    REQUIRED. Loại token được cấp như mô tả trong Phần 7.1. Giá trị không phân biệt chữ hoa, chữ thường.
    
- expires_in
    
    RECOMMENDED. Thời gian tồn tại tính bằng giây của access token. Ví dụ, giá trị "3600" biểu thị rằng access token sẽ hết hạn trong một giờ kể từ thời điểm phản hồi được tạo. Nếu bị bỏ qua, authorization server NÊN cung cấp thời gian hết hạn bằng các phương tiện khác hoặc ghi lại giá trị mặc định.
    
- refresh_token
    
    OPTIONAL. Refresh token, có thể được sử dụng để có được các access tokens mới bằng cách sử dụng cùng một authorization grant như mô tả trong Phần 6.
    
- scope
    
    OPTIONAL, nếu giống hệt với scope được client yêu cầu; nếu không, REQUIRED. Scope của access token như mô tả trong Phần 3.3.
    

Các tham số được bao gồm trong **entity-body** của phản hồi **HTTP** bằng cách sử dụng kiểu media "**application/json**" như được định nghĩa bởi [RFC4627]. Các tham số được tuần tự hóa thành một cấu trúc **JavaScript Object Notation (JSON)** bằng cách thêm từng tham số ở cấp cấu trúc cao nhất. Tên tham số và giá trị chuỗi được bao gồm dưới dạng chuỗi **JSON**. Các giá trị số được bao gồm dưới dạng số **JSON**. Thứ tự của các tham số không quan trọng và có thể thay đổi.

Ví dụ:

JSON

`HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8
Cache-Control: no-store
Pragma: no-cache

{
  "access_token":"2YotnFZFEjr1zCsicMWpAA",
  "token_type":"example",
  "expires_in":3600,
  "refresh_token":"tGzv3JOkF0XG5Qx2TlKWIA",
  "example_parameter":"example_value"
}`

**Client PHẢI** bỏ qua các tên giá trị không được nhận dạng trong phản hồi. Kích thước của **tokens** và các giá trị khác nhận được từ **authorization server** không được định nghĩa. **Client** nên tránh đưa ra các giả định về kích thước giá trị. **Authorization server NÊN** ghi lại kích thước của bất kỳ giá trị nào mà nó cấp.

---

### 5.2. Error Response

**Authorization server** phản hồi với mã trạng thái **HTTP 400 (Bad Request)** (trừ khi được chỉ định khác) và bao gồm các tham số sau với phản hồi:

- error
    
    REQUIRED. Một error code ASCII [USASCII] duy nhất từ các loại sau:
    
    - invalid_request
        
        Yêu cầu thiếu một tham số bắt buộc, bao gồm một giá trị tham số không được hỗ trợ (khác với grant type), lặp lại một tham số, bao gồm nhiều credentials, sử dụng nhiều hơn một cơ chế để xác thực client, hoặc bị định dạng sai.
        
    - invalid_client
        
        Xác thực client thất bại (ví dụ: client không xác định, không bao gồm xác thực client, hoặc phương thức xác thực không được hỗ trợ). Authorization server CÓ THỂ trả về mã trạng thái HTTP 401 (Unauthorized) để chỉ ra các lược đồ xác thực HTTP được hỗ trợ. Nếu client cố gắng xác thực thông qua trường tiêu đề yêu cầu "Authorization", authorization server PHẢI phản hồi bằng mã trạng thái HTTP 401 (Unauthorized) và bao gồm trường tiêu đề phản hồi "WWW-Authenticate" khớp với lược đồ xác thực được client sử dụng.
        
    - invalid_grant
        
        Authorization grant được cung cấp (ví dụ: authorization code, resource owner credentials) hoặc refresh token không hợp lệ, đã hết hạn, bị thu hồi, không khớp với redirection URI được sử dụng trong authorization request, hoặc được cấp cho một client khác.
        
    - unauthorized_client
        
        Client đã xác thực không được ủy quyền để sử dụng loại authorization grant này.
        
    - unsupported_grant_type
        
        Loại authorization grant không được authorization server hỗ trợ.
        
    - invalid_scope
        
        Requested scope không hợp lệ, không xác định, bị định dạng sai, hoặc vượt quá scope được resource owner cấp.
        
    
    Các giá trị cho tham số "**error**" **KHÔNG ĐƯỢC** bao gồm các ký tự ngoài tập hợp %x20-21 / %x23-5B / %x5D-7E.
    
- error_description
    
    OPTIONAL. Văn bản ASCII [USASCII] dễ đọc cung cấp thông tin bổ sung, được sử dụng để hỗ trợ client developer trong việc hiểu lỗi đã xảy ra. Các giá trị cho tham số "error_description" KHÔNG ĐƯỢC bao gồm các ký tự ngoài tập hợp %x20-21 / %x23-5B / %x5D-7E.
    
- error_uri
    
    OPTIONAL. Một URI xác định một trang web dễ đọc với thông tin về lỗi, được sử dụng để cung cấp cho client developer thông tin bổ sung về lỗi. Các giá trị cho tham số "error_uri" PHẢI tuân thủ cú pháp URI-reference và do đó KHÔNG ĐƯỢC bao gồm các ký tự ngoài tập hợp %x21 / %x23-5B / %x5D-7E.
    

Các tham số được bao gồm trong **entity-body** của phản hồi **HTTP** bằng cách sử dụng kiểu media "**application/json**" như được định nghĩa bởi [RFC4627]. Các tham số được tuần tự hóa thành một cấu trúc **JSON** bằng cách thêm từng tham số ở cấp cấu trúc cao nhất. Tên tham số và giá trị chuỗi được bao gồm dưới dạng chuỗi **JSON**. Các giá trị số được bao gồm dưới dạng số **JSON**. Thứ tự của các tham số không quan trọng và có thể thay đổi.

Ví dụ:

JSON

`HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8
Cache-Control: no-store
Pragma: no-cache

{
  "error":"invalid_request"
}`

---

## 6. Refreshing an Access Token

Nếu **authorization server** cấp một **refresh token** cho **client**, **client** thực hiện một yêu cầu **refresh** đến **token endpoint** bằng cách thêm các tham số sau bằng định dạng "**application/x-www-form-urlencoded**" theo Phụ lục B với mã hóa ký tự **UTF-8** trong **HTTP request entity-body**:

- grant_type
    
    REQUIRED. Giá trị PHẢI được đặt thành "refresh_token".
    
- refresh_token
    
    REQUIRED. Refresh token được cấp cho client.
    
- scope
    
    OPTIONAL. Scope của yêu cầu truy cập như mô tả trong Phần 3.3. Requested scope KHÔNG ĐƯỢC bao gồm bất kỳ scope nào không được resource owner cấp ban đầu, và nếu bị bỏ qua, nó được coi là bằng scope được resource owner cấp ban đầu.
    

Bởi vì **refresh tokens** thường là các **credentials** có thời gian tồn tại dài được sử dụng để yêu cầu các **access tokens** bổ sung, **refresh token** được gắn với **client** mà nó đã được cấp. Nếu **client type** là **confidential** hoặc **client** được cấp **client credentials** (hoặc được gán các yêu cầu xác thực khác), **client PHẢI** xác thực với **authorization server** như mô tả trong Phần 3.2.1.

Ví dụ, **client** thực hiện yêu cầu **HTTP** sau bằng **transport-layer security** (có thêm ngắt dòng chỉ để hiển thị):

`POST /token HTTP/1.1
Host: server.example.com
Authorization: Basic czZCaGRSa3F0MzpnWDFmQmF0M2JW
Content-Type: application/x-www-form-urlencoded

grant_type=refresh_token&refresh_token=tGzv3JOkF0XG5Qx2TlKWIA`

**Authorization server PHẢI**:

- yêu cầu xác thực **client** cho các **confidential clients** hoặc cho bất kỳ **client** nào đã được cấp **client credentials** (hoặc với các yêu cầu xác thực khác),
- xác thực **client** nếu xác thực **client** được bao gồm và đảm bảo rằng **refresh token** đã được cấp cho **client** đã xác thực, và
- xác nhận **refresh token**.

Nếu hợp lệ và được ủy quyền, **authorization server** cấp một **access token** như mô tả trong Phần 5.1. Nếu yêu cầu xác minh thất bại hoặc không hợp lệ, **authorization server** trả về một **error response** như mô tả trong Phần 5.2.

**Authorization server CÓ THỂ** cấp một **refresh token** mới, trong trường hợp đó **client PHẢI** loại bỏ **refresh token** cũ và thay thế nó bằng **refresh token** mới. **Authorization server CÓ THỂ** thu hồi **refresh token** cũ sau khi cấp một **refresh token** mới cho **client**. Nếu một **refresh token** mới được cấp, **refresh token scope PHẢI** giống hệt với **scope** của **refresh token** được **client** bao gồm trong yêu cầu.

---

## 7. Accessing Protected Resources

**Client** truy cập các **protected resources** bằng cách trình bày **access token** cho **resource server**. **Resource server PHẢI** xác nhận **access token** và đảm bảo rằng nó chưa hết hạn và **scope** của nó bao gồm **requested resource**. Các phương pháp được **resource server** sử dụng để xác nhận **access token** (cũng như bất kỳ **error responses** nào) nằm ngoài phạm vi của đặc tả này nhưng thường liên quan đến một tương tác hoặc phối hợp giữa **resource server** và **authorization server**.

Phương pháp mà **client** sử dụng **access token** để xác thực với **resource server** phụ thuộc vào loại **access token** được cấp bởi **authorization server**. Thông thường, nó liên quan đến việc sử dụng trường tiêu đề yêu cầu **HTTP "Authorization"** [RFC2617] với một lược đồ xác thực được định nghĩa bởi đặc tả của loại **access token** được sử dụng, chẳng hạn như [RFC6750].

### 7.1. Access Token Types

Loại **access token** cung cấp cho **client** thông tin cần thiết để sử dụng thành công **access token** để thực hiện yêu cầu **protected resource** (cùng với các thuộc tính cụ thể theo loại). **Client KHÔNG ĐƯỢC** sử dụng một **access token** nếu nó không hiểu loại **token**.

Ví dụ, loại **token "bearer"** được định nghĩa trong [RFC6750] được sử dụng bằng cách đơn giản bao gồm chuỗi **access token** trong yêu cầu:

`GET /resource/1 HTTP/1.1
Host: example.com
Authorization: Bearer mF_9.B5f-4.1JqM`

trong khi loại **token "mac"** được định nghĩa trong [OAuth-HTTP-MAC] được sử dụng bằng cách cấp một khóa **Message Authentication Code (MAC)** cùng với **access token** được sử dụng để ký các thành phần nhất định của các yêu cầu **HTTP**:

`GET /resource/1 HTTP/1.1
Host: example.com
Authorization: MAC id="h480djs93hd8",
                   nonce="274312:dj83hs9s",
                   mac="kDZvddkndxvhGRXZhvuDjEWhGeE="`

Các ví dụ trên chỉ được cung cấp cho mục đích minh họa. Các nhà phát triển được khuyến nghị tham khảo các đặc tả [RFC6750] và [OAuth-HTTP-MAC] trước khi sử dụng.

Mỗi định nghĩa loại **access token** chỉ định các thuộc tính bổ sung (nếu có) được gửi đến **client** cùng với tham số phản hồi "**access_token**". Nó cũng định nghĩa phương thức xác thực **HTTP** được sử dụng để bao gồm **access token** khi thực hiện yêu cầu **protected resource**.

### 7.2. Error Response

Nếu một yêu cầu truy cập **resource** thất bại, **resource server NÊN** thông báo cho **client** về lỗi. Mặc dù các chi tiết cụ thể của các phản hồi lỗi như vậy nằm ngoài phạm vi của đặc tả này, tài liệu này thiết lập một **registry** chung trong Phần 11.4 cho các giá trị lỗi được chia sẻ giữa các lược đồ xác thực **OAuth token**.

Các lược đồ xác thực mới được thiết kế chủ yếu cho xác thực **OAuth token NÊN** định nghĩa một cơ chế để cung cấp mã trạng thái lỗi cho **client**, trong đó các giá trị lỗi được phép được đăng ký trong **error registry** được thiết lập bởi đặc tả này.

Các lược đồ như vậy **CÓ THỂ** giới hạn tập hợp các mã lỗi hợp lệ thành một tập hợp con của các giá trị đã đăng ký. Nếu **error code** được trả về bằng một tham số có tên, tên tham số **NÊN** là "**error**".

Các lược đồ khác có khả năng được sử dụng cho xác thực **OAuth token**, nhưng không được thiết kế chủ yếu cho mục đích đó, **CÓ THỂ** liên kết các giá trị lỗi của chúng với **registry** theo cùng một cách.

Các lược đồ xác thực mới **CÓ THỂ** chọn cũng chỉ định việc sử dụng các tham số "**error_description**" và "**error_uri**" để trả về thông tin lỗi theo cách song song với việc sử dụng chúng trong đặc tả này.

---

## 8. Extensibility

### 8.1. Defining Access Token Types

Các loại **access token** có thể được định nghĩa theo một trong hai cách: đăng ký trong **Access Token Types registry** (theo các quy trình trong Phần 11.1), hoặc bằng cách sử dụng một **absolute URI** duy nhất làm tên của nó.

Các loại sử dụng tên **URI NÊN** được giới hạn cho các triển khai dành riêng cho nhà cung cấp mà không phổ biến, và cụ thể cho các chi tiết triển khai của **resource server** nơi chúng được sử dụng.

Tất cả các loại khác **PHẢI** được đăng ký. Tên loại **PHẢI** tuân thủ **type-name ABNF**. Nếu định nghĩa loại bao gồm một lược đồ xác thực **HTTP** mới, tên loại **NÊN** giống hệt tên lược đồ xác thực **HTTP** (như được định nghĩa bởi [RFC2617]). Loại **token "example"** được dành riêng để sử dụng trong các ví dụ.

`type-name  = 1*name-char
name-char  = "-" / "." / "_" / DIGIT / ALPHA`

### 8.2. Defining New Endpoint Parameters

Các tham số yêu cầu hoặc phản hồi mới để sử dụng với **authorization endpoint** hoặc **token endpoint** được định nghĩa và đăng ký trong **OAuth Parameters registry** theo quy trình trong Phần 11.2.

Tên tham số **PHẢI** tuân thủ **param-name ABNF**, và cú pháp giá trị tham số **PHẢI** được định nghĩa rõ ràng (ví dụ: sử dụng **ABNF**, hoặc một tham chiếu đến cú pháp của một tham số hiện có).

`param-name  = 1*name-char
name-char   = "-" / "." / "_" / DIGIT / ALPHA`

Các tiện ích mở rộng tham số dành riêng cho nhà cung cấp chưa được đăng ký mà không phổ biến và cụ thể cho các chi tiết triển khai của **authorization server** nơi chúng được sử dụng **NÊN** sử dụng một tiền tố dành riêng cho nhà cung cấp mà không có khả năng xung đột với các giá trị đã đăng ký khác (ví dụ: bắt đầu bằng 'companyname_').

### 8.3. Defining New Authorization Grant Types

Các loại **authorization grant** mới có thể được định nghĩa bằng cách gán cho chúng một **absolute URI** duy nhất để sử dụng với tham số "**grant_type**". Nếu loại **extension grant** yêu cầu các tham số **token endpoint** bổ sung, chúng **PHẢI** được đăng ký trong **OAuth Parameters registry** như mô tả trong Phần 11.2.

### 8.4. Defining New Authorization Endpoint Response Types

Các loại phản hồi mới để sử dụng với **authorization endpoint** được định nghĩa và đăng ký trong **Authorization Endpoint Response Types registry** theo quy trình trong Phần 11.3. Tên loại phản hồi **PHẢI** tuân thủ **response-type ABNF**.

`response-type  = response-name *( SP response-name )
response-name  = 1*response-char
response-char  = "_" / DIGIT / ALPHA`

Nếu một **response type** chứa một hoặc nhiều ký tự dấu cách (%x20), nó được so sánh dưới dạng một danh sách các giá trị được phân tách bằng dấu cách trong đó thứ tự của các giá trị không quan trọng. Chỉ một thứ tự các giá trị có thể được đăng ký, bao gồm tất cả các sắp xếp khác của cùng một tập hợp các giá trị.

Ví dụ, loại phản hồi "**token code**" không được định nghĩa bởi đặc tả này. Tuy nhiên, một tiện ích mở rộng có thể định nghĩa và đăng ký loại phản hồi "**token code**". Sau khi được đăng ký, sự kết hợp tương tự không thể được đăng ký là "**code token**", nhưng cả hai giá trị đều có thể được sử dụng để chỉ cùng một loại phản hồi.

### 8.5. Defining Additional Error Codes

Trong các trường hợp mà các tiện ích mở rộng giao thức (tức là **access token types**, **extension parameters**, hoặc **extension grant types**) yêu cầu các **error codes** bổ sung được sử dụng với **authorization code grant error response** (Phần 4.1.2.1), **implicit grant error response** (Phần 4.2.2.1), **token error response** (Phần 5.2), hoặc **resource access error response** (Phần 7.2), các **error codes** đó **CÓ THỂ** được định nghĩa.

Các **extension error codes PHẢI** được đăng ký (theo các quy trình trong Phần 11.4) nếu tiện ích mở rộng mà chúng được sử dụng cùng là một loại **access token** đã đăng ký, một tham số **endpoint** đã đăng ký, hoặc một loại **extension grant**. Các **error codes** được sử dụng với các tiện ích mở rộng chưa đăng ký **CÓ THỂ** được đăng ký.

Các **error codes PHẢI** tuân thủ **error ABNF** và **NÊN** được thêm tiền tố bằng một tên nhận dạng khi có thể. Ví dụ, một lỗi nhận dạng một giá trị không hợp lệ được đặt cho tham số tiện ích mở rộng "**example**" **NÊN** được đặt tên là "**example_invalid**".

`error      = 1*error-char
error-char = %x20-21 / %x23-5B / %x5D-7E`

---

## 9. Native Applications

**Native applications** là các **clients** được cài đặt và thực thi trên thiết bị được **resource owner** sử dụng (ví dụ: ứng dụng **desktop**, ứng dụng **mobile native**). **Native applications** yêu cầu xem xét đặc biệt liên quan đến bảo mật, khả năng nền tảng và trải nghiệm tổng thể của người dùng cuối.

**Authorization endpoint** yêu cầu tương tác giữa **client** và **user-agent** của **resource owner**. **Native applications** có thể gọi một **user-agent** bên ngoài hoặc nhúng một **user-agent** bên trong ứng dụng. Ví dụ:

- **External user-agent** - **native application** có thể bắt giữ phản hồi từ **authorization server** bằng cách sử dụng **redirection URI** với một lược đồ được đăng ký với hệ điều hành để gọi **client** làm trình xử lý, sao chép và dán **credentials** thủ công, chạy một **web server** cục bộ, cài đặt một tiện ích mở rộng **user-agent**, hoặc bằng cách cung cấp một **redirection URI** xác định một **server-hosted resource** dưới sự kiểm soát của **client**, sau đó cung cấp phản hồi cho **native application**.
- **Embedded user-agent** - **native application** có được phản hồi bằng cách giao tiếp trực tiếp với **embedded user-agent** bằng cách giám sát các thay đổi trạng thái phát ra trong quá trình tải **resource**, hoặc truy cập bộ nhớ **cookies** của **user-agent**.

Khi lựa chọn giữa **external** hoặc **embedded user-agent**, các nhà phát triển nên xem xét những điều sau:

- Một **external user-agent** có thể cải thiện tỷ lệ hoàn thành, vì **resource owner** có thể đã có một phiên hoạt động với **authorization server**, loại bỏ nhu cầu xác thực lại. Nó cung cấp trải nghiệm và chức năng quen thuộc cho người dùng cuối. **Resource owner** cũng có thể dựa vào các tính năng hoặc tiện ích mở rộng của **user-agent** để hỗ trợ xác thực (ví dụ: trình quản lý mật khẩu, trình đọc thiết bị 2 yếu tố).
- Một **embedded user-agent** có thể mang lại khả năng sử dụng được cải thiện, vì nó loại bỏ nhu cầu chuyển đổi ngữ cảnh và mở cửa sổ mới.
- Một **embedded user-agent** đặt ra một thách thức bảo mật vì **resource owners** đang xác thực trong một cửa sổ không xác định mà không có quyền truy cập vào các biện pháp bảo vệ trực quan được tìm thấy trong hầu hết các **external user-agents**. Một **embedded user-agent** giáo dục người dùng cuối tin tưởng các yêu cầu xác thực không xác định (làm cho các cuộc tấn công **phishing** dễ thực hiện hơn).

Khi lựa chọn giữa **implicit grant type** và **authorization code grant type**, những điều sau nên được xem xét:

- **Native applications** sử dụng **authorization code grant type NÊN** làm như vậy mà không sử dụng **client credentials**, do **native application** không có khả năng giữ **client credentials confidential**.
- Khi sử dụng luồng **implicit grant type**, một **refresh token** không được trả về, điều này yêu cầu lặp lại quá trình ủy quyền sau khi **access token** hết hạn.

---

## 10. Security Considerations

Là một khuôn khổ linh hoạt và có thể mở rộng, các cân nhắc bảo mật của OAuth phụ thuộc vào nhiều yếu tố. Các phần sau đây cung cấp cho những người triển khai các hướng dẫn bảo mật tập trung vào ba **client profiles** được mô tả trong Phần 2.1: **web application**, **user-agent-based application**, và **native application**.

Một mô hình và phân tích bảo mật OAuth toàn diện, cũng như nền tảng cho thiết kế giao thức, được cung cấp bởi [OAuth-THREATMODEL].

### 10.1. Client Authentication

**Authorization server** thiết lập **client credentials** với các **web application clients** cho mục đích xác thực **client**. **Authorization server** được khuyến khích xem xét các phương tiện xác thực **client** mạnh hơn password **client**. **Web application clients PHẢI** đảm bảo tính bảo mật của **client passwords** và các **client credentials** khác.

**Authorization server KHÔNG ĐƯỢC** cấp **client passwords** hoặc các **client credentials** khác cho **native application** hoặc **user-agent-based application clients** cho mục đích xác thực **client**. **Authorization server CÓ THỂ** cấp một **client password** hoặc các **credentials** khác cho một cài đặt cụ thể của một **native application client** trên một thiết bị cụ thể.

Khi xác thực **client** không thể thực hiện được, **authorization server NÊN** sử dụng các phương tiện khác để xác nhận danh tính của **client** -- ví dụ, bằng cách yêu cầu đăng ký **client redirection URI** hoặc yêu cầu **resource owner** xác nhận danh tính. Một **redirection URI** hợp lệ là không đủ để xác minh danh tính của **client** khi yêu cầu ủy quyền **resource owner** nhưng có thể được sử dụng để ngăn chặn việc gửi **credentials** đến một **client** giả mạo sau khi có được ủy quyền **resource owner**.

**Authorization server** phải xem xét các tác động bảo mật của việc tương tác với các **unauthenticated clients** và thực hiện các biện pháp để hạn chế khả năng phơi bày các **credentials** khác (ví dụ: **refresh tokens**) được cấp cho các **clients** đó.

### 10.2. Client Impersonation

Một **malicious client** có thể mạo danh một **client** khác và có được quyền truy cập vào các **protected resources** nếu **client** bị mạo danh thất bại trong việc, hoặc không thể, giữ **client credentials** của mình **confidential**.

**Authorization server PHẢI** xác thực **client** bất cứ khi nào có thể. Nếu **authorization server** không thể xác thực **client** do bản chất của **client**, **authorization server PHẢI** yêu cầu đăng ký bất kỳ **redirection URI** nào được sử dụng để nhận phản hồi ủy quyền và **NÊN** sử dụng các phương tiện khác để bảo vệ **resource owners** khỏi các **malicious clients** tiềm tàng như vậy. Ví dụ, **authorization server** có thể yêu cầu **resource owner** hỗ trợ trong việc xác định **client** và nguồn gốc của nó.

**Authorization server NÊN** thực thi xác thực **resource owner** rõ ràng và cung cấp cho **resource owner** thông tin về **client** và **authorization scope** và thời gian tồn tại được yêu cầu. **Resource owner** có trách nhiệm xem xét thông tin trong ngữ cảnh của **client** hiện tại và ủy quyền hoặc từ chối yêu cầu.

**Authorization server KHÔNG ĐƯỢC** tự động xử lý các yêu cầu ủy quyền lặp lại (không có sự tương tác chủ động của **resource owner**) mà không xác thực **client** hoặc dựa vào các biện pháp khác để đảm bảo rằng yêu cầu lặp lại đến từ **client** gốc chứ không phải là kẻ mạo danh.

### 10.3. Access Tokens

**Access token credentials** (cũng như bất kỳ thuộc tính **access token confidential** nào) **PHẢI** được giữ **confidential** trong quá trình truyền và lưu trữ, và chỉ được chia sẻ giữa **authorization server**, các **resource servers** mà **access token** hợp lệ, và **client** mà **access token** được cấp. **Access token credentials CHỈ ĐƯỢC** truyền bằng **TLS** như mô tả trong Phần 1.6 với xác thực **server** như được định nghĩa bởi [RFC2818].

Khi sử dụng **implicit grant type**, **access token** được truyền trong **URI fragment**, điều này có thể làm lộ nó cho các bên không được ủy quyền.

**Authorization server PHẢI** đảm bảo rằng **access tokens** không thể được tạo, sửa đổi hoặc đoán để tạo ra các **access tokens** hợp lệ bởi các bên không được ủy quyền.

**Client NÊN** yêu cầu **access tokens** với **scope** tối thiểu cần thiết. **Authorization server NÊN** xem xét danh tính **client** khi lựa chọn cách thực hiện **requested scope** và **CÓ THỂ** cấp một **access token** với ít quyền hơn so với yêu cầu.

Đặc tả này không cung cấp bất kỳ phương pháp nào để **resource server** đảm bảo rằng một **access token** được trình bày cho nó bởi một **client** nhất định đã được cấp cho **client** đó bởi **authorization server**.

### 10.4. Refresh Tokens

**Authorization servers CÓ THỂ** cấp **refresh tokens** cho các **web application clients** và **native application clients**.

**Refresh tokens PHẢI** được giữ **confidential** trong quá trình truyền và lưu trữ, và chỉ được chia sẻ giữa **authorization server** và **client** mà **refresh tokens** được cấp. **Authorization server PHẢI** duy trì mối liên kết giữa một **refresh token** và **client** mà nó đã được cấp. **Refresh tokens CHỈ ĐƯỢC** truyền bằng **TLS** như mô tả trong Phần 1.6 với xác thực **server** như được định nghĩa bởi [RFC2818].

**Authorization server PHẢI** xác minh mối liên kết giữa **refresh token** và danh tính **client** bất cứ khi nào danh tính **client** có thể được xác thực. Khi xác thực **client** không thể thực hiện được, **authorization server NÊN** triển khai các phương tiện khác để phát hiện lạm dụng **refresh token**.

Ví dụ, **authorization server** có thể sử dụng **refresh token rotation** trong đó một **refresh token** mới được cấp với mỗi phản hồi **access token refresh**. **Refresh token** trước đó bị vô hiệu hóa nhưng được **authorization server** giữ lại. Nếu một **refresh token** bị xâm phạm và sau đó được sử dụng bởi cả kẻ tấn công và **client** hợp pháp, một trong số họ sẽ trình bày một **refresh token** đã bị vô hiệu hóa, điều này sẽ thông báo cho **authorization server** về vi phạm.

**Authorization server PHẢI** đảm bảo rằng **refresh tokens** không thể được tạo, sửa đổi hoặc đoán để tạo ra các **refresh tokens** hợp lệ bởi các bên không được ủy quyền.

### 10.5. Authorization Codes

Việc truyền **authorization codes NÊN** được thực hiện qua một kênh bảo mật, và **client NÊN** yêu cầu sử dụng **TLS** với **redirection URI** của nó nếu **URI** xác định một tài nguyên mạng. Vì **authorization codes** được truyền qua **user-agent redirections**, chúng có thể bị tiết lộ thông qua lịch sử **user-agent** và tiêu đề **HTTP referrer**.

**Authorization codes** hoạt động như các **plaintext bearer credentials**, được sử dụng để xác minh rằng **resource owner** đã cấp ủy quyền tại **authorization server** là cùng một **resource owner** quay trở lại **client** để hoàn tất quá trình. Do đó, nếu **client** dựa vào **authorization code** để xác thực **resource owner** của chính nó, **client redirection endpoint PHẢI** yêu cầu sử dụng **TLS**.

**Authorization codes PHẢI** có thời gian tồn tại ngắn và chỉ được sử dụng một lần. Nếu **authorization server** quan sát thấy nhiều lần cố gắng trao đổi một **authorization code** để lấy một **access token**, **authorization server NÊN** cố gắng thu hồi tất cả các **access tokens** đã được cấp dựa trên **authorization code** bị xâm phạm.

Nếu **client** có thể được xác thực, **authorization servers PHẢI** xác thực **client** và đảm bảo rằng **authorization code** đã được cấp cho cùng một **client**.

---

### 10.6. Thao Tác URI Chuyển Hướng Mã Ủy Quyền (Authorization Code Redirection URI Manipulation)

Khi yêu cầu ủy quyền bằng cách sử dụng loại **grant** mã ủy quyền (**authorization code grant type**), **client** có thể chỉ định một **redirection URI** thông qua tham số "**redirect_uri**". Nếu kẻ tấn công có thể thao túng giá trị của **redirection URI**, nó có thể khiến **authorization server** chuyển hướng **user-agent** của **resource owner** đến một **URI** nằm dưới sự kiểm soát của kẻ tấn công cùng với **authorization code**.

Một kẻ tấn công có thể tạo một tài khoản tại một **client** hợp pháp và khởi tạo luồng ủy quyền. Khi **user-agent** của kẻ tấn công được gửi đến **authorization server** để cấp quyền truy cập, kẻ tấn công sẽ lấy **authorization URI** được cung cấp bởi **client** hợp pháp và thay thế **redirection URI** của **client** bằng một **URI** nằm dưới sự kiểm soát của kẻ tấn công. Sau đó, kẻ tấn công lừa nạn nhân nhấp vào liên kết đã bị thao túng để ủy quyền truy cập vào **client** hợp pháp.

Khi đến **authorization server**, nạn nhân được nhắc nhở với một yêu cầu bình thường, hợp lệ thay mặt cho một **client** hợp pháp và đáng tin cậy, và ủy quyền yêu cầu. Sau đó, nạn nhân được chuyển hướng đến một **endpoint** nằm dưới sự kiểm soát của kẻ tấn công cùng với **authorization code**. Kẻ tấn công hoàn tất luồng ủy quyền bằng cách gửi **authorization code** cho **client** bằng **redirection URI** gốc được cung cấp bởi **client**. **Client** trao đổi **authorization code** để lấy một **access token** và liên kết nó với tài khoản **client** của kẻ tấn công, tài khoản này giờ đây có thể truy cập các **protected resources** được nạn nhân ủy quyền (thông qua **client**).

Để ngăn chặn cuộc tấn công như vậy, **authorization server PHẢI** đảm bảo rằng **redirection URI** được sử dụng để lấy **authorization code** giống hệt với **redirection URI** được cung cấp khi trao đổi **authorization code** để lấy một **access token**. **Authorization server PHẢI** yêu cầu các **public clients** và **NÊN** yêu cầu các **confidential clients** đăng ký **redirection URIs** của họ. Nếu một **redirection URI** được cung cấp trong yêu cầu, **authorization server PHẢI** xác nhận nó so với giá trị đã đăng ký.

---

### 10.7. Resource Owner Password Credentials

Loại **grant** **resource owner password credentials** thường được sử dụng vì lý do **legacy** hoặc chuyển đổi. Nó làm giảm rủi ro tổng thể khi lưu trữ **usernames** và **passwords** bởi **client** nhưng không loại bỏ nhu cầu phơi bày các **highly privileged credentials** cho **client**.

Loại **grant** này mang rủi ro cao hơn các loại **grant** khác vì nó duy trì **password anti-pattern** mà giao thức này tìm cách tránh. **Client** có thể lạm dụng password, hoặc password có thể vô tình bị tiết lộ cho kẻ tấn công (ví dụ: thông qua các tệp nhật ký hoặc các bản ghi khác do **client** lưu giữ).

Ngoài ra, vì **resource owner** không kiểm soát quá trình ủy quyền (sự tham gia của **resource owner** kết thúc khi nó giao **credentials** của mình cho **client**), **client** có thể có được các **access tokens** với **scope** rộng hơn mong muốn của **resource owner**. **Authorization server** nên xem xét **scope** và thời gian tồn tại của các **access tokens** được cấp thông qua loại **grant** này.

**Authorization server** và **client NÊN** giảm thiểu việc sử dụng loại **grant** này và sử dụng các loại **grant** khác bất cứ khi nào có thể.

---

### 10.8. Yêu Cầu Bảo Mật (Request Confidentiality)

**Access tokens**, **refresh tokens**, **resource owner passwords**, và **client credentials KHÔNG ĐƯỢC** được truyền đi mà không mã hóa. **Authorization codes KHÔNG NÊN** được truyền đi mà không mã hóa.

Các tham số "**state**" và "**scope**" **KHÔNG NÊN** bao gồm thông tin nhạy cảm của **client** hoặc **resource owner** dưới dạng văn bản thuần túy, vì chúng có thể được truyền qua các kênh không an toàn hoặc lưu trữ không an toàn.

---

### 10.9. Đảm Bảo Tính Xác Thực của Endpoint (Ensuring Endpoint Authenticity)

Để ngăn chặn các cuộc tấn công **man-in-the-middle**, **authorization server PHẢI** yêu cầu sử dụng **TLS** với xác thực **server** như được định nghĩa bởi [RFC2818] cho bất kỳ yêu cầu nào được gửi đến các **authorization** và **token endpoints**. **Client PHẢI** xác nhận chứng chỉ **TLS** của **authorization server** như được định nghĩa bởi [RFC6125] và theo các yêu cầu của nó về xác thực danh tính **server**.

---

### 10.10. Tấn Công Đoán Credentials (Credentials-Guessing Attacks)

**Authorization server PHẢI** ngăn chặn kẻ tấn công đoán **access tokens**, **authorization codes**, **refresh tokens**, **resource owner passwords**, và **client credentials**.

Xác suất kẻ tấn công đoán các **tokens** được tạo (và các **credentials** khác không dành cho người dùng cuối xử lý) **PHẢI** nhỏ hơn hoặc bằng 2^(-128) và **NÊN** nhỏ hơn hoặc bằng 2^(-160).

**Authorization server PHẢI** sử dụng các phương tiện khác để bảo vệ các **credentials** dành cho người dùng cuối.

---

### 10.11. Tấn Công Lừa Đảo (Phishing Attacks)

Việc triển khai rộng rãi giao thức này và các giao thức tương tự có thể khiến người dùng cuối trở nên quen với việc bị chuyển hướng đến các trang web nơi họ được yêu cầu nhập mật khẩu của mình. Nếu người dùng cuối không cẩn thận xác minh tính xác thực của các trang web này trước khi nhập **credentials** của họ, kẻ tấn công sẽ có thể khai thác thực hành này để đánh cắp mật khẩu của **resource owners**.

Các nhà cung cấp dịch vụ nên cố gắng giáo dục người dùng cuối về các rủi ro mà các cuộc tấn công **phishing** gây ra và nên cung cấp các cơ chế giúp người dùng cuối dễ dàng xác nhận tính xác thực của các trang web của họ. Các nhà phát triển **client** nên xem xét các tác động bảo mật của cách họ tương tác với **user-agent** (ví dụ: bên ngoài, nhúng) và khả năng của người dùng cuối trong việc xác minh tính xác thực của **authorization server**.

Để giảm rủi ro tấn công **phishing**, các **authorization servers PHẢI** yêu cầu sử dụng **TLS** trên mọi **endpoint** được sử dụng cho tương tác người dùng cuối.

---

### 10.12. Tấn Công Giả Mạo Yêu Cầu Đa Trang (Cross-Site Request Forgery)

**Cross-site request forgery (CSRF)** là một hành vi khai thác trong đó kẻ tấn công khiến **user-agent** của nạn nhân người dùng cuối truy cập một **URI** độc hại (ví dụ: được cung cấp cho **user-agent** dưới dạng một liên kết, hình ảnh hoặc chuyển hướng gây hiểu lầm) đến một **server** đáng tin cậy (thường được thiết lập thông qua sự hiện diện của một **session cookie** hợp lệ).

Một cuộc tấn công **CSRF** chống lại **redirection URI** của **client** cho phép kẻ tấn công chèn **authorization code** hoặc **access token** của riêng nó, điều này có thể dẫn đến việc **client** sử dụng một **access token** được liên kết với các **protected resources** của kẻ tấn công thay vì của nạn nhân (ví dụ: lưu thông tin tài khoản ngân hàng của nạn nhân vào một **protected resource** do kẻ tấn công kiểm soát).

**Client PHẢI** triển khai bảo vệ **CSRF** cho **redirection URI** của nó. Điều này thường được thực hiện bằng cách yêu cầu bất kỳ yêu cầu nào được gửi đến **redirection URI endpoint** phải bao gồm một giá trị liên kết yêu cầu với trạng thái xác thực của **user-agent** (ví dụ: một **hash** của **session cookie** được sử dụng để xác thực **user-agent**). **Client NÊN** sử dụng tham số yêu cầu "**state**" để gửi giá trị này đến **authorization server** khi thực hiện yêu cầu ủy quyền.

Sau khi ủy quyền đã được cấp từ người dùng cuối, **authorization server** chuyển hướng **user-agent** của người dùng cuối trở lại **client** với giá trị liên kết cần thiết có trong tham số "**state**". Giá trị liên kết cho phép **client** xác minh tính hợp lệ của yêu cầu bằng cách khớp giá trị liên kết với trạng thái xác thực của **user-agent**. Giá trị liên kết được sử dụng để bảo vệ **CSRF PHẢI** chứa một giá trị không thể đoán được (như mô tả trong Phần 10.10), và trạng thái xác thực của **user-agent** (ví dụ: **session cookie**, **HTML5 local storage**) **PHẢI** được giữ ở một vị trí chỉ có thể truy cập được bởi **client** và **user-agent** (tức là được bảo vệ bởi **same-origin policy**).

Một cuộc tấn công **CSRF** chống lại **authorization endpoint** của **authorization server** có thể dẫn đến việc kẻ tấn công có được ủy quyền của người dùng cuối cho một **malicious client** mà không có sự tham gia hoặc cảnh báo của người dùng cuối.

**Authorization server PHẢI** triển khai bảo vệ **CSRF** cho **authorization endpoint** của nó và đảm bảo rằng một **malicious client** không thể có được ủy quyền mà không có sự nhận biết và đồng ý rõ ràng của **resource owner**.

---

### 10.13. Clickjacking

Trong một cuộc tấn công **clickjacking**, kẻ tấn công đăng ký một **client** hợp pháp và sau đó xây dựng một trang web độc hại trong đó nó tải trang web **authorization endpoint** của **authorization server** trong một **iframe** trong suốt được phủ lên trên một tập hợp các nút giả, được xây dựng cẩn thận để đặt trực tiếp dưới các nút quan trọng trên trang ủy quyền. Khi người dùng cuối nhấp vào một nút hiển thị gây hiểu lầm, người dùng cuối thực sự đang nhấp vào một nút vô hình trên trang ủy quyền (chẳng hạn như nút "**Authorize**"). Điều này cho phép kẻ tấn công lừa **resource owner** cấp quyền truy cập cho **client** của mình mà người dùng cuối không hề hay biết.

Để ngăn chặn hình thức tấn công này, các **native applications NÊN** sử dụng các trình duyệt bên ngoài thay vì nhúng trình duyệt bên trong ứng dụng khi yêu cầu ủy quyền người dùng cuối. Đối với hầu hết các trình duyệt mới hơn, việc tránh **iframes** có thể được thực thi bởi **authorization server** bằng cách sử dụng tiêu đề (không chuẩn) "**x-frame-options**". Tiêu đề này có thể có hai giá trị, "**deny**" và "**sameorigin**", sẽ chặn bất kỳ **framing** nào, hoặc **framing** bởi các trang web có nguồn gốc khác, tương ứng. Đối với các trình duyệt cũ hơn, các kỹ thuật **JavaScript frame-busting** có thể được sử dụng nhưng có thể không hiệu quả trong tất cả các trình duyệt.

---

### 10.14. Tiêm Mã và Xác Thực Đầu Vào (Code Injection and Input Validation)

Một cuộc tấn công **code injection** xảy ra khi một đầu vào hoặc biến bên ngoài khác được một ứng dụng sử dụng mà không được làm sạch và gây ra sửa đổi logic ứng dụng. Điều này có thể cho phép kẻ tấn công có được quyền truy cập vào thiết bị ứng dụng hoặc dữ liệu của nó, gây ra từ chối dịch vụ, hoặc gây ra một loạt các tác dụng phụ độc hại.

**Authorization server** và **client PHẢI** làm sạch (và xác nhận khi có thể) bất kỳ giá trị nào nhận được -- đặc biệt, giá trị của các tham số "**state**" và "**redirect_uri**".

---

### 10.15. Trình Chuyển Hướng Mở (Open Redirectors)

**Authorization server**, **authorization endpoint**, và **client redirection endpoint** có thể bị cấu hình sai và hoạt động như các **open redirectors**. Một **open redirector** là một **endpoint** sử dụng một tham số để tự động chuyển hướng một **user-agent** đến vị trí được chỉ định bởi giá trị tham số mà không có bất kỳ xác nhận nào.

Các **open redirectors** có thể được sử dụng trong các cuộc tấn công **phishing**, hoặc bởi kẻ tấn công để khiến người dùng cuối truy cập các trang web độc hại bằng cách sử dụng thành phần **URI authority** của một đích đến quen thuộc và đáng tin cậy. Ngoài ra, nếu **authorization server** cho phép **client** chỉ đăng ký một phần của **redirection URI**, kẻ tấn công có thể sử dụng một **open redirector** do **client** vận hành để xây dựng một **redirection URI** sẽ vượt qua xác nhận của **authorization server** nhưng sẽ gửi **authorization code** hoặc **access token** đến một **endpoint** nằm dưới sự kiểm soát của kẻ tấn công.

---

### 10.16. Lạm Dụng Access Token để Mạo Danh Resource Owner trong Luồng Implicit (Misuse of Access Token to Impersonate Resource Owner in Implicit Flow)

Đối với các **public clients** sử dụng các luồng **implicit**, đặc tả này không cung cấp bất kỳ phương pháp nào để **client** xác định **client** nào đã được cấp một **access token**.

Một **resource owner** có thể tự nguyện ủy quyền truy cập vào một **resource** bằng cách cấp một **access token** cho **malicious client** của kẻ tấn công. Điều này có thể là do **phishing** hoặc một số lý do khác. Kẻ tấn công cũng có thể đánh cắp một **token** thông qua một cơ chế khác. Kẻ tấn công sau đó có thể cố gắng mạo danh **resource owner** bằng cách cung cấp **access token** cho một **public client** hợp pháp.

Trong luồng **implicit** (**response_type=token**), kẻ tấn công có thể dễ dàng thay đổi **token** trong phản hồi từ **authorization server**, thay thế **access token** thật bằng **token** đã được cấp trước đó cho kẻ tấn công.

Các **servers** giao tiếp với các **native applications** dựa vào việc được truyền một **access token** trong kênh sau (**back channel**) để xác định người dùng của **client** có thể bị xâm phạm tương tự bởi một kẻ tấn công tạo ra một ứng dụng bị xâm phạm có thể chèn các **access tokens** bị đánh cắp tùy ý.

Bất kỳ **public client** nào cho rằng chỉ **resource owner** mới có thể trình bày cho nó một **access token** hợp lệ cho **resource** đều dễ bị tấn công loại này.

Loại tấn công này có thể làm lộ thông tin về **resource owner** tại **client** hợp pháp cho kẻ tấn công (**malicious client**). Điều này cũng sẽ cho phép kẻ tấn công thực hiện các hoạt động tại **client** hợp pháp với cùng các quyền như **resource owner** đã cấp **access token** hoặc **authorization code** ban đầu.

Xác thực **resource owners** cho **clients** nằm ngoài phạm vi của đặc tả này. Bất kỳ đặc tả nào sử dụng quá trình ủy quyền như một hình thức xác thực người dùng cuối ủy quyền cho **client** (ví dụ: dịch vụ đăng nhập bên thứ ba) **KHÔNG ĐƯỢC** sử dụng luồng **implicit** mà không có các cơ chế bảo mật bổ sung cho phép **client** xác định xem **access token** có được cấp để sử dụng cho nó hay không (ví dụ: **audience-restricting the access token**).

---

## 11. IANA Considerations

### 11.1. OAuth Access Token Types Registry

Đặc tả này thiết lập **OAuth Access Token Types registry**.

Các loại **access token** được đăng ký với **Specification Required** ([RFC5226]) sau thời gian xem xét hai tuần trên danh sách gửi thư **oauth-ext-review@ietf.org**, theo lời khuyên của một hoặc nhiều **Designated Experts**. Tuy nhiên, để cho phép phân bổ giá trị trước khi xuất bản, **Designated Expert(s)** có thể chấp thuận đăng ký khi họ hài lòng rằng một đặc tả như vậy sẽ được xuất bản.

Các yêu cầu đăng ký phải được gửi đến danh sách gửi thư **oauth-ext-review@ietf.org** để xem xét và bình luận, với một chủ đề thích hợp (ví dụ: "Request for access token type: example").

Trong thời gian xem xét, **Designated Expert(s)** sẽ chấp thuận hoặc từ chối yêu cầu đăng ký, thông báo quyết định này cho danh sách xem xét và IANA. Các quyết định từ chối nên bao gồm giải thích và, nếu có thể, các gợi ý về cách thực hiện yêu cầu thành công.

IANA chỉ phải chấp nhận các cập nhật **registry** từ **Designated Expert(s)** và nên chuyển tất cả các yêu cầu đăng ký đến danh sách gửi thư xem xét.

#### 11.1.1. Registration Template

- Type name:
    
    Tên được yêu cầu (ví dụ: "example").
    
- Additional Token Endpoint Response Parameters:
    
    Các tham số phản hồi bổ sung được trả về cùng với tham số "access_token". Các tham số mới PHẢI được đăng ký riêng trong OAuth Parameters registry như mô tả trong Phần 11.2.
    
- HTTP Authentication Scheme(s):
    
    Tên lược đồ xác thực HTTP, nếu có, được sử dụng để xác thực các yêu cầu protected resource bằng cách sử dụng các access tokens thuộc loại này.
    
- Change controller:
    
    Đối với Standards Track RFCs, ghi "IETF". Đối với các trường hợp khác, ghi tên của bên chịu trách nhiệm. Các chi tiết khác (ví dụ: địa chỉ bưu điện, địa chỉ email, home page URI) cũng có thể được bao gồm.
    
- Specification document(s):
    
    Tham chiếu đến (các) tài liệu chỉ định tham số, tốt nhất là bao gồm một URI có thể được sử dụng để truy xuất bản sao của (các) tài liệu. Một chỉ dẫn về các phần liên quan cũng có thể được bao gồm nhưng không bắt buộc.
    

---

#### 11.2. OAuth Parameters Registry

Đặc tả này thiết lập **OAuth Parameters registry**.

Các tham số bổ sung để đưa vào yêu cầu **authorization endpoint**, phản hồi **authorization endpoint**, yêu cầu **token endpoint**, hoặc phản hồi **token endpoint** được đăng ký với **Specification Required** ([RFC5226]) sau thời gian xem xét hai tuần trên danh sách gửi thư **oauth-ext-review@ietf.org**, theo lời khuyên của một hoặc nhiều **Designated Experts**. Tuy nhiên, để cho phép phân bổ giá trị trước khi xuất bản, **Designated Expert(s)** có thể chấp thuận đăng ký khi họ hài lòng rằng một đặc tả như vậy sẽ được xuất bản.

Các yêu cầu đăng ký phải được gửi đến danh sách gửi thư **oauth-ext-review@ietf.org** để xem xét và bình luận, với một chủ đề thích hợp (ví dụ: "Request for parameter: example").

Trong thời gian xem xét, **Designated Expert(s)** sẽ chấp thuận hoặc từ chối yêu cầu đăng ký, thông báo quyết định này cho danh sách xem xét và IANA. Các quyết định từ chối nên bao gồm giải thích và, nếu có thể, các gợi ý về cách thực hiện yêu cầu thành công.

IANA chỉ phải chấp nhận các cập nhật **registry** từ **Designated Expert(s)** và nên chuyển tất cả các yêu cầu đăng ký đến danh sách gửi thư xem xét.

#### 11.2.1. Registration Template

- Parameter name:
    
    Tên được yêu cầu (ví dụ: "example").
    
- Parameter usage location:
    
    Vị trí (các) tham số có thể được sử dụng. Các vị trí có thể là authorization request, authorization response, token request, hoặc token response.
    
- Change controller:
    
    Đối với Standards Track RFCs, ghi "IETF". Đối với các trường hợp khác, ghi tên của bên chịu trách nhiệm. Các chi tiết khác (ví dụ: địa chỉ bưu điện, địa chỉ email, home page URI) cũng có thể được bao gồm.
    
- Specification document(s):
    
    Tham chiếu đến (các) tài liệu chỉ định tham số, tốt nhất là bao gồm một URI có thể được sử dụng để truy xuất bản sao của (các) tài liệu. Một chỉ dẫn về các phần liên quan cũng có thể được bao gồm nhưng không bắt buộc.
    

#### 11.2.2. Initial Registry Contents

Nội dung ban đầu của **OAuth Parameters registry** là:

- **Parameter name**: **client_id**
- **Parameter usage location**: **authorization request**, **token request**
- **Change controller**: IETF
- **Specification document(s)**: RFC 6749
- **Parameter name**: **client_secret**
- **Parameter usage location**: **token request**
- **Change controller**: IETF
- **Specification document(s)**: RFC 6749
- **Parameter name**: **response_type**
- **Parameter usage location**: **authorization request**
- **Change controller**: IETF
- **Specification document(s)**: RFC 6749
- **Parameter name**: **redirect_uri**
- **Parameter usage location**: **authorization request**, **token request**
- **Change controller**: IETF
- **Specification document(s)**: RFC 6749
- **Parameter name**: **scope**
- **Parameter usage location**: **authorization request**, **authorization response**, **token request**, **token response**
- **Change controller**: IETF
- **Specification document(s)**: RFC 6749
- **Parameter name**: **state**
- **Parameter usage location**: **authorization request**, **authorization response**
- **Change controller**: IETF
- **Specification document(s)**: RFC 6749
- **Parameter name**: **code**
- **Parameter usage location**: **authorization response**, **token request**
- **Change controller**: IETF
- **Specification document(s)**: RFC 6749
- **Parameter name**: **error_description**
- **Parameter usage location**: **authorization response**, **token response**
- **Change controller**: IETF
- **Specification document(s)**: RFC 6749
- **Parameter name**: **error_uri**
- **Parameter usage location**: **authorization response**, **token response**
- **Change controller**: IETF
- **Specification document(s)**: RFC 6749
- **Parameter name**: **grant_type**
- **Parameter usage location**: **token request**
- **Change controller**: IETF
- **Specification document(s)**: RFC 6749
- **Parameter name**: **access_token**
- **Parameter usage location**: **authorization response**, **token response**
- **Change controller**: IETF
- **Specification document(s)**: RFC 6749
- **Parameter name**: **token_type**
- **Parameter usage location**: **authorization response**, **token response**
- **Change controller**: IETF
- **Specification document(s)**: RFC 6749
- **Parameter name**: **expires_in**
- **Parameter usage location**: **authorization response**, **token response**
- **Change controller**: IETF
- **Specification document(s)**: RFC 6749
- **Parameter name**: **username**
- **Parameter usage location**: **token request**
- **Change controller**: IETF
- **Specification document(s)**: RFC 6749
- **Parameter name**: **password**
- **Parameter usage location**: **token request**
- **Change controller**: IETF
- **Specification document(s)**: RFC 6749
- **Parameter name**: **refresh_token**
- **Parameter usage location**: **token request**, **token response**
- **Change controller**: IETF
- **Specification document(s)**: RFC 6749

---

### 11.3. OAuth Authorization Endpoint Response Types Registry

Đặc tả này thiết lập **OAuth Authorization Endpoint Response Types registry**.

Các loại phản hồi bổ sung để sử dụng với **authorization endpoint** được đăng ký với **Specification Required** ([RFC5226]) sau thời gian xem xét hai tuần trên danh sách gửi thư **oauth-ext-review@ietf.org**, theo lời khuyên của một hoặc nhiều **Designated Experts**. Tuy nhiên, để cho phép phân bổ giá trị trước khi xuất bản, **Designated Expert(s)** có thể chấp thuận đăng ký khi họ hài lòng rằng một đặc tả như vậy sẽ được xuất bản.

Các yêu cầu đăng ký phải được gửi đến danh sách gửi thư **oauth-ext-review@ietf.org** để xem xét và bình luận, với một chủ đề thích hợp (ví dụ: "Request for response type: example").

Trong thời gian xem xét, **Designated Expert(s)** sẽ chấp thuận hoặc từ chối yêu cầu đăng ký, thông báo quyết định này cho danh sách xem xét và IANA. Các quyết định từ chối nên bao gồm giải thích và, nếu có thể, các gợi ý về cách thực hiện yêu cầu thành công.

IANA chỉ phải chấp nhận các cập nhật **registry** từ **Designated Expert(s)** và nên chuyển tất cả các yêu cầu đăng ký đến danh sách gửi thư xem xét.

#### 11.3.1. Registration Template

- Response type name:
    
    Tên được yêu cầu (ví dụ: "example").
    
- Change controller:
    
    Đối với Standards Track RFCs, ghi "IETF". Đối với các trường hợp khác, ghi tên của bên chịu trách nhiệm. Các chi tiết khác (ví dụ: địa chỉ bưu điện, địa chỉ email, home page URI) cũng có thể được bao gồm.
    
- Specification document(s):
    
    Tham chiếu đến (các) tài liệu chỉ định loại, tốt nhất là bao gồm một URI có thể được sử dụng để truy xuất bản sao của (các) tài liệu. Một chỉ dẫn về các phần liên quan cũng có thể được bao gồm nhưng không bắt buộc.
    

#### 11.3.2. Initial Registry Contents

Nội dung ban đầu của **OAuth Authorization Endpoint Response Types registry** là:

- **Response type name**: **code**
- **Change controller**: IETF
- **Specification document(s)**: RFC 6749
- **Response type name**: **token**
- **Change controller**: IETF
- **Specification document(s)**: RFC 6749

---

### 11.4. OAuth Extensions Error Registry

Đặc tả này thiết lập **OAuth Extensions Error registry**.

Các mã lỗi bổ sung được sử dụng cùng với các tiện ích mở rộng giao thức khác (tức là **extension grant types**, **access token types**, hoặc **extension parameters**) được đăng ký với **Specification Required** ([RFC5226]) sau thời gian xem xét hai tuần trên danh sách gửi thư **oauth-ext-review@ietf.org**, theo lời khuyên của một hoặc nhiều **Designated Experts**. Tuy nhiên, để cho phép phân bổ giá trị trước khi xuất bản, **Designated Expert(s)** có thể chấp thuận đăng ký khi họ hài lòng rằng một đặc tả như vậy sẽ được xuất bản.

Các yêu cầu đăng ký phải được gửi đến danh sách gửi thư **oauth-ext-review@ietf.org** để xem xét và bình luận, với một chủ đề thích hợp (ví dụ: "Request for error code: example").

Trong thời gian xem xét, **Designated Expert(s)** sẽ chấp thuận hoặc từ chối yêu cầu đăng ký, thông báo quyết định này cho danh sách xem xét và IANA. Các quyết định từ chối nên bao gồm giải thích và, nếu có thể, các gợi ý về cách thực hiện yêu cầu thành công.

IANA chỉ phải chấp nhận các cập nhật **registry** từ **Designated Expert(s)** và nên chuyển tất cả các yêu cầu đăng ký đến danh sách gửi thư xem xét.

#### 11.4.1. Registration Template

- Error name:
    
    Tên được yêu cầu (ví dụ: "example"). Các giá trị cho tên lỗi KHÔNG ĐƯỢC bao gồm các ký tự ngoài tập hợp %x20-21 / %x23-5B / %x5D-7E.
    
- Error usage location:
    
    Vị trí (các) lỗi có thể được sử dụng. Các vị trí có thể là authorization code grant error response (Phần 4.1.2.1), implicit grant error response (Phần 4.2.2.1), token error response (Phần 5.2), hoặc resource access error response (Phần 7.2).
    
- Related protocol extension:
    
    Tên của loại extension grant, loại access token, hoặc tham số mở rộng mà error code được sử dụng cùng.
    
- Change controller:
    
    Đối với Standards Track RFCs, ghi "IETF". Đối với các trường hợp khác, ghi tên của bên chịu trách nhiệm. Các chi tiết khác (ví dụ: địa chỉ bưu điện, địa chỉ email, home page URI) cũng có thể được bao gồm.
    
- Specification document(s):
    
    Tham chiếu đến (các) tài liệu chỉ định error code, tốt nhất là bao gồm một URI có thể được sử dụng để truy xuất bản sao của (các) tài liệu. Một chỉ dẫn về các phần liên quan cũng có thể được bao gồm nhưng không bắt buộc.
