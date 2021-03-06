---
ms.openlocfilehash: a393cf978318c39081805cae7e38c3386ff156f5
ms.sourcegitcommit: 225e4b45844e845bc41d5c043587a61e6b6ce5ae
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/11/2021
ms.locfileid: "103010693"
---
| Jazyk/rozhraní | Projekt zapnut<br/>GitHubu                                                                                                    | Balíček                                                                      | Úvod<br/>Začínáme                             | Přihlášení uživatelů                                         | Přístup k webovým rozhraním API                                                 | Všeobecně dostupná (GA) *nebo*<br/>Verze Public Preview<sup>1</sup> |
|----------------------|--------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------|:-----------------------------------------------:|:-----------------------------------------------------:|:---------------------------------------------------------------:|:------------------------------------------------------------:|
| Angular              | [MSAL úhlová v2](https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-angular)<sup>2</sup>         | [@azure/msal-angular](https://www.npmjs.com/package/@azure/msal-angular)     | —                                               | ![Knihovna může vyžádat tokeny ID pro přihlášení uživatele.][y] | ![Knihovna může požadovat přístupové tokeny pro chráněná webová rozhraní API.][y] | Verze Public Preview                                               |
| Angular              | [MSAL úhlová](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/msal-angular-v1/lib/msal-angular)<sup>3</sup> | [@azure/msal-angular](https://www.npmjs.com/package/@azure/msal-angular)     |[Kurz](../articles/active-directory/develop/tutorial-v2-angular.md)| ![Knihovna může vyžádat tokeny ID pro přihlášení uživatele.][y] | ![Knihovna může požadovat přístupové tokeny pro chráněná webová rozhraní API.][y] | GA                                                           |
| AngularJS            | [MSAL AngularJS](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/lib/msal-angularjs)<sup>3</sup>         | [@azure/msal-angularjs](https://www.npmjs.com/package/@azure/msal-angularjs) | —                                               | ![Knihovna může vyžádat tokeny ID pro přihlášení uživatele.][y] | ![Knihovna může požadovat přístupové tokeny pro chráněná webová rozhraní API.][y] | Verze Public Preview                                               |
| JavaScript           | [MSAL.js v2](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/lib/msal-browser)<sup>2</sup>              | [@azure/msal-browser](https://www.npmjs.com/package/@azure/msal-browser)     | [Kurz](../articles/active-directory/develop/tutorial-v2-javascript-auth-code.md) | ![Knihovna může vyžádat tokeny ID pro přihlášení uživatele.][y] | ![Knihovna může požadovat přístupové tokeny pro chráněná webová rozhraní API.][y] | GA                                                           |
|JavaScript|[MSAL.js 1,0](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/lib/msal-core)<sup>3</sup> | [@azure/msal-core](https://www.npmjs.com/package/@azure/msal-core)    | [Kurz](../articles/active-directory/develop/tutorial-v2-javascript-spa.md)| ![Knihovna může vyžádat tokeny ID pro přihlášení uživatele.][y] | ![Knihovna může požadovat přístupové tokeny pro chráněná webová rozhraní API.][y] | GA                                                           |
| React                | [MSAL reagují](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/lib/msal-react)<sup>2</sup>                 | [@azure/msal-react](https://www.npmjs.com/package/@azure/msal-react)         | —                                               | ![Knihovna může vyžádat tokeny ID pro přihlášení uživatele.][y] | ![Knihovna může požadovat přístupové tokeny pro chráněná webová rozhraní API.][y] | Verze Public Preview                                               |
<!--
| Vue | [Vue MSAL]( https://github.com/mvertopoulos/vue-msal) | [vue-msal]( https://www.npmjs.com/package/vue-msal) | ![X indicating no.][n] | ![Green check mark.][y] | ![Green check mark.][y] | -- |
-->

<sup>1</sup> [dodatečné podmínky použití pro Microsoft Azure][preview-tos] Preview se vztahují na knihovny ve *verzi Public Preview*.

<sup>2</sup> [tok ověřovacího kódu][auth-code-flow] jenom s PCKE (doporučeno) 

<sup>3</sup> jenom [implicitní tok udělení][implicit-flow] .

<!--Image references-->

[y]: ../articles/active-directory/develop/media/common/yes.png
[n]: ../articles/active-directory/develop/media/common/no.png

<!--Reference-style links -->
[AAD-App-Model-V2-Overview]: v2-overview.md
[Microsoft-SDL]: https://www.microsoft.com/securityengineering/sdl/
[preview-tos]: https://azure.microsoft.com/support/legal/preview-supplemental-terms/
[auth-code-flow]: ../articles/active-directory/develop/v2-oauth2-auth-code-flow.md
[implicit-flow]: ../articles/active-directory/develop/v2-oauth2-implicit-grant-flow.md