# 🌭 D-TO
> **개인 맞춤형 접근성 최적화 커머스 플랫폼**

---

## 👥 1. Team Information
**"안녕하세요 팀2 D-TO입니다."**

| 직책 | 성명 | 담당 업무 |
| :--- | :--- | :--- |
| **Total PM / PL** | **이지수** | **프로젝트 총괄 , DB 설계(ERD), API 명세 확립 및 통합 관리** |
| **Team Member** | **전이레** | Frontend / Backend Development |
| **Team Member** | **정인혁** | Frontend / Backend Development |

---

## 🛠 2. Tech Stack
- **Backend:** Java 17, Spring Boot, Spring Security, JPA, Oracle Cloud DB
- **Frontend:** React, JavaScript
- **Infrastructure/Etc:** Toss Payments API, JWT, GitHub Actions

---

## 📊 3. Full API Specification (Total List)

| 섹션 | API 명칭 | Method | 엔드포인트 | Request Body (JSON) | 비고 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **1. 인증** | 회원가입 | `POST` | `/api/auth/signup` | `{"email": "s", "password": "s", "name": "s"}` | |
|      | 로그인 | `POST` | `/api/auth/login` | `{"email": "s", "password": "s"}` | JWT 발급 |
|      | 프로필 조회 | `GET` | `/api/members/me` | `(None)` | 마이페이지 |
|      | 배송지 추가 | `POST` | `/api/members/addresses` | `{"zipCode": "s", "baseAddress": "s", "detailAddress": "s", ...}` | |
| **2. 접근성** | 설정 조회 | `GET` | `/api/accessibility` | `(None)` | **개인화 UI 근거** |
|      | 설정 업데이트 | `PUT` | `/api/accessibility` | `{"fontSizeStep": n, "highContrastEnabled": b, ...}` | |
| **3. 상품** | 목록/검색 | `GET` | `/api/products` | `(?category=HEALTH&keyword=s&page=n)` | **맞춤형 큐레이션** |
|      | 상세 조회 | `GET` | `/api/products/{id}` | `(None)` | 대체텍스트 포함 |
| **4. 장바구니** | 목록 조회 | `GET` | `/api/carts` | `(None)` | |
|      | 상품 추가 | `POST` | `/api/carts` | `{"productId": n, "quantity": n}` | |
|      | 수량 수정 | `PATCH` | `/api/carts/{id}` | `{"quantity": n}` | |
|      | 상품 삭제 | `DELETE` | `/api/carts/{id}` | `(None)` | |
| **5. 주문** | 주문 생성 | `POST` | `/api/orders` | `{"cartIdList": n[], "addressId": n}` | PENDING 생성 |
|      | 결제 승인 | `POST` | `/api/payments/confirm` | `{"paymentKey": "s", "orderId": n, "amount": n}` | 토스 연동 |
|      | 내 주문 내역 | `GET` | `/api/orders` | `(?page=n)` | |
| **6. 리뷰** | 리뷰 조회 | `GET` | `/api/reviews` | `(?productId=n)` | |
|      | 리뷰 작성 | `POST` | `/api/reviews` | `{"productId": n, "orderId": n, "rating": n, "content": "s"}` | |
| **7. 관리자** | 상품 등록/수정 | `POST/PUT` | `/api/admin/products` | `{"name": "s", "price": n, "altText": "s", ...}` | **Admin 전용** |
|      | 회원/주문 관리 | `GET/PATCH` | `/api/admin/...` | `{"role": "s", "status": "s"}` | **Admin 전용** |
| **공통** | 이미지 업로드 | `POST` | `/api/common/images` | `(MultipartFile)` | 이미지 서버 저장 |

---

## 🔗 4. Core Architecture
- **ERD 기반 설계**: 모든 테이블 구조는 사용자의 접근성 설정과 카테고리 선호를 최우선으로 반영함.
- **개인화 로직**: 로그인 시 유저의 `accessibility_settings`를 즉시 반영하여 폰트 및 고대비 모드 전환.
- **보안**: Spring Security를 통한 일반 유저와 관리자(`ROLE_ADMIN`)의 API 접근 권한 분리.

---
© 2026 D-TO Project Team. All rights reserved.
