---
title: '자습서: Infinite Campus와 Azure Active Directory 통합 | Microsoft Docs'
description: Azure Active Directory 및 Infinite Campus 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 3995b544-e751-4e0f-ab8b-c9a3862da6ba
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/30/2018
ms.author: jeedes
ms.collection: M365-identity-device-management
ms.openlocfilehash: e0ada3055a3347cb42179fddbba671f2f03f502d
ms.sourcegitcommit: 5839af386c5a2ad46aaaeb90a13065ef94e61e74
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2019
ms.locfileid: "57885070"
---
# <a name="tutorial-azure-active-directory-integration-with-infinite-campus"></a>자습서: Infinite Campus와 Azure Active Directory 통합

이 자습서에서는 Azure AD(Azure Active Directory)와 Infinite Campus를 통합하는 방법에 대해 알아봅니다.

Infinite Campus를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.

- Infinite Campus에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.
- 사용자가 해당 Azure AD 계정으로 Infinite Campus에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.
- 단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.

Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 애플리케이션 액세스 및 Single Sign-On이란 무엇인가요?](../manage-apps/what-is-single-sign-on.md)를 참조하세요.

## <a name="prerequisites"></a>필수 조건

Infinite Campus와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.

- Azure AD 구독
- 무한 캠퍼스에서 single sign-on이 설정 된 구독

> [!NOTE]
> 이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.

이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.

- 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.
- Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.
- 최소한 캠퍼스 제품 보안 역할의 "학생 정보 시스템 (SIS)" 구성을 완료 하려면 Azure Active Directory 관리자가 될를 해야 합니다.

## <a name="scenario-description"></a>시나리오 설명

이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.  이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.

1. 갤러리에서 Infinite Campus 추가
2. Azure AD Single Sign-on 구성 및 테스트

## <a name="adding-infinite-campus-from-the-gallery"></a>갤러리에서 Infinite Campus 추가

Infinite Campus의 Azure AD 통합을 구성하려면 갤러리의 Infinite Campus를 관리되는 SaaS 앱 목록에 추가해야 합니다.

**갤러리에서 Infinite Campus를 추가하려면 다음 단계를 수행합니다.**

1. **[Azure Portal](https://portal.azure.com)** 의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다. 

    ![Azure Active Directory 단추][1]

2. **엔터프라이즈 애플리케이션**으로 이동합니다. 그런 후 **모든 애플리케이션**으로 이동합니다.

    ![엔터프라이즈 애플리케이션 블레이드][2]

3. 새 애플리케이션을 추가하려면 대화 상자 맨 위 있는 **새 애플리케이션** 단추를 클릭합니다.

    ![새 애플리케이션 단추][3]

4. 검색 상자에 **Infinite Campus**를 입력하고 결과 패널에서 **Infinite Campus**를 선택한 후 **추가** 단추를 클릭하여 애플리케이션을 추가합니다.

    ![결과 목록의 Infinite Campus](./media/infinitecampus-tutorial/tutorial_infinitecampus_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성 및 테스트

이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Infinite Campus에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Infinite Campus 사용자가 누구인지 알고 있어야 합니다. 즉, Azure AD 사용자와 Infinite Campus의 관련 사용자 간에 연결이 형성되어야 합니다.

Infinite Campus에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.
2. **[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On 테스트하는 데 사용합니다.
3. **[무한 캠퍼스 테스트 사용자 만들기](#creating-a-infinite-campus-test-user)**  -Britta simon 이라는 사용자를 Azure AD 표현과 연결 되는 무한 캠퍼스 합니다.
4. **[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.
5. **[Single Sign-On 테스트](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성

이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Infinite Campus 애플리케이션에서 Single Sign-On을 구성합니다.

**Infinite Campus에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**

1. Azure Portal의 **Infinite Campus** 애플리케이션 통합 페이지에서 **Single Sign-On**을 클릭합니다.

    ![Single Sign-On 구성 링크][4]

2. **Single Sign-On 방법 선택** 대화 상자에서 **SAML** 모드에 대해 **선택**을 클릭하여 Single Sign-On을 사용하도록 설정합니다.

    ![Configure Single Sign-On](common/tutorial_general_301.png)

3. **SAML로 Single Sign-On 설정** 페이지에서 **편집** 아이콘을 클릭하여 **기본 SAML 구성** 대화 상자를 엽니다.

    ![Configure Single Sign-On](common/editconfigure.png)

4. 에 **기본 SAML 구성** 섹션에 있는 경우를 **서비스 공급자 메타 데이터 파일** 완료 무한 캠퍼스에서 내보낸 4.a 4.d 통해 단계 및 11.c 단계를 건너뜁니다. 서비스 공급자 메타 데이터 파일이 없는 경우 5단계로 건너뜁니다.

    a. **메타데이터 파일 업로드**를 클릭합니다.

        ![image](common/b9_saml.png)

    b. **폴더 로고**를 클릭하여 메타데이터 파일을 선택하고 **업로드**를 클릭합니다.

    ![이미지](common/b9(1)_saml.png)

    다. 메타데이터 파일이 정상적으로 업로드되면 아래 그림과 같이 **기본 SAML 구성** 섹션에서 **식별자** 및 **회신 URL** 값이 자동으로 입력됩니다.

    ![이미지](./media/infinitecampus-tutorial/tutorial_infinitecampus_url.png)

    d. **로그온 URL** 텍스트 상자에 다음 패턴을 사용하여 URL을 입력합니다(도메인은 호스팅 모델에 따라 다름).`https://<DOMAIN>.infinitecampus.com/campus/SSO/<DISTRICTNAME>/SIS`

5. **서비스 공급자 메타데이터 파일**이 없는 경우 다음 단계를 수행합니다(도메인은 호스팅 모델에 따라 달라짐).

    a. **로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<DOMAIN>.infinitecampus.com/campus/SSO/<DISTRICTNAME>/SIS`

    b. **식별자** 텍스트 상자에서 `https://<DOMAIN>.infinitecampus.com/campus/<DISTRICTNAME>` 패턴을 사용하여 URL을 입력합니다.

    다. **회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.`https://<DOMAIN>.infinitecampus.com/campus/SSO/<DISTRICTNAME>`

    ![Infinite Campus 도메인 및 URL Single Sign-On 정보](./media/infinitecampus-tutorial/tutorial_infinitecampus_url1.png)

6. **SAML 서명 인증서** 페이지의 **SAML 서명 인증서** 섹션에서 복사 **아이콘**을 클릭하여  **앱 페더레이션 메타데이터 URL** 을 복사하고 메모장에 붙여넣습니다.

    ![인증서 다운로드 링크](./media/infinitecampus-tutorial/tutorial_infinitecampus_certificate.png) 

7. **Infinite Campus 설정** 섹션에서 다음 값을 사용하여 Azure 메타데이터 파일/URL을 업로드하거나 활용할 때 유효성을 검사합니다.

    a. 로그인 URL

    b. Azure AD 식별자

    다. 로그아웃 URL

    ![Infinite Campus 구성](common/configuresection.png)

8. 다른 웹 브라우저 창에서 Infinite Campus에 보안 관리자 권한으로 로그인합니다.

9. 왼쪽 메뉴에서 **시스템 관리**를 클릭합니다.

    ![관리자](./media/infinitecampus-tutorial/tutorial_infinitecampus_admin.png)

10. **사용자 보안** > **SAML 관리** > **SSO 서비스 공급자 구성**으로 이동합니다.

    ![saml](./media/infinitecampus-tutorial/tutorial_infinitecampus_saml.png)

11. **SSO 서비스 공급자 구성** 페이지에서 다음 단계를 수행합니다.

    ![sso](./media/infinitecampus-tutorial/tutorial_infinitecampus_sso.png)

    a. **SAML Single Sign-On 사용**을 선택합니다.
    
    b. 편집 된 **선택적 특성 이름** 포함할 **이름**
    
    다. 에 **IDP (Id 공급자) 서버 데이터를 검색 하는 옵션을 선택** 섹션을 선택 합니다 **메타 데이터 URL**를 붙여 합니다 **앱 페더레이션 메타 데이터 Url** (6 단계 위의)에서 클릭 한 다음 확인 하 고 상자에 **동기화**합니다.

    d. **서비스 공급 기업 메타데이터** 링크를 클릭하여 **서비스 공급 기업 메타데이터 파일**을 컴퓨터에 저장하고 **기본 SAML 구성** 섹션에 업로드합니다. 그러면 Azure Portal에서 **식별자** 및 **회신 URL** 값이 자동으로 입력됩니다(값의 업로드 및 자동 입력은 4단계를 참조하거나 수동 입력은 5단계를 참조하세요).

    e. **동기화**를 클릭하면 값이 **SSO 서비스 공급자 구성** 페이지에 자동으로 입력됩니다.

    f. **저장**을 클릭합니다.

### <a name="creating-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기

이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 _단일_ 테스트 사용자를 만드는 것입니다.

1. Azure Portal의 왼쪽 창에서 **Azure Active Directory**, **사용자**를 차례로 선택하고 **모든 사용자**를 선택합니다.

    ![Azure AD 사용자 만들기][100]

2. 화면 위쪽에서 **새 사용자**를 선택합니다.

    ![Azure AD 테스트 사용자 만들기](common/create_aaduser_01.png) 

3. 사용자 속성에서 다음 단계를 수행합니다.

    ![Azure AD 테스트 사용자 만들기](common/create_aaduser_02.png)

    a. **이름** 필드에 **BrittaSimon**을 입력합니다.
  
    b. 에 **사용자 이름** 필드에 입력 **brittasimon\@yourcompanydomain.extension**  
    예를 들어 BrittaSimon@contoso.com

    다. **속성**을 선택하고 **암호 표시** 확인란을 선택한 다음, 암호 상자에 표시된 값을 적어 둡니다.

    d. **만들기**를 선택합니다.

### <a name="creating-an-infinite-campus-test-user"></a>무한 캠퍼스 테스트 사용자 만들기

Infinite Campus는 인구 통계 기반 아키텍처입니다. Infinite Campus 플랫폼에 사용자를 추가하려면 [Infinite Campus 지원 팀](mailto:sales@infinitecampus.com)에 문의하세요.

### <a name="assigning-the-azure-ad-test-user"></a>Azure AD 테스트 사용자 할당

이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Infinite Campus에 대한 액세스 권한을 부여합니다.

1. Azure Portal에서 **엔터프라이즈 애플리케이션**을 선택한 다음, **모든 애플리케이션**을 선택합니다.

    ![사용자 할당][201]

2. 애플리케이션 목록에서 **Infinite Campus**를 선택합니다.

    ![Configure Single Sign-On](./media/infinitecampus-tutorial/tutorial_infinitecampus_app.png) 

3. 왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.

    ![사용자 할당][202]

4. **추가** 단추를 클릭합니다. 그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.

    ![사용자 할당][203]

5. **사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택하고 화면 아래쪽에서 **선택** 단추를 클릭합니다.

6. **할당 추가** 대화 상자에서 **할당** 단추를 선택합니다.

### <a name="testing-single-sign-on"></a>Single Sign-On 테스트

이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.

액세스 패널에서 Infinite Campus 타일을 클릭하면 Infinite Campus 애플리케이션에 자동으로 로그온됩니다. Azure AD를 관리 하는 동일한 브라우저에서 무한 캠퍼스 응용 프로그램에 기록 하는 경우 테스트 사용자를 Azure AD 로그인을 확인 합니다. 액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](../user-help/active-directory-saas-access-panel-introduction.md)를 참조하세요.

## <a name="additional-resources"></a>추가 리소스

* [Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록](tutorial-list.md)
* [Azure Active Directory로 애플리케이션 액세스 및 Single Sign-On을 구현하는 방법](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: common/tutorial_general_01.png
[2]: common/tutorial_general_02.png
[3]: common/tutorial_general_03.png
[4]: common/tutorial_general_04.png

[100]: common/tutorial_general_100.png

[201]: common/tutorial_general_201.png
[202]: common/tutorial_general_202.png
[203]: common/tutorial_general_203.png
