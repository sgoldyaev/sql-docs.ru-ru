---
title: "ОТМЕНИТЕ разрешения Full-Text (Transact-SQL) | Документы Microsoft"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- REVOKE statement, full-text permissions
- full-text catalogs [SQL Server], permissions
- full-text stoplist [SQL Server], permissions
ms.assetid: ef617436-1e86-4573-900a-702e27a202b9
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 33348a7ee48835021143507175165b27fde4b74a
ms.contentlocale: ru-ru
ms.lasthandoff: 09/01/2017

---
# <a name="revoke-full-text-permissions-transact-sql"></a>REVOKE, отмена разрешений на полнотекстовые объекты (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Отменяет разрешения на полнотекстовый каталог или список полнотекстовых стоп-слов.  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
REVOKE [ GRANT OPTION FOR ] permission [ ,...n ] ON  
    FULLTEXT   
        {  
           CATALOG :: full-text_catalog_name  
           |  
           STOPLIST :: full-text_stoplist_name  
        }  
    { TO | FROM } database_principal [ ,...n ]  
    [ CASCADE ]  
    [ AS revoking_principal ]  
```  
  
## <a name="arguments"></a>Аргументы  
 GRANT OPTION FOR  
 Показывает, что отменяется право на предоставление указанного разрешения другим участникам. Само разрешение отменено не будет.  
  
> [!IMPORTANT]  
>  Если участник обладает указанным разрешением без параметра GRANT, будет отменено само разрешение.  
  
 *разрешение*  
 Имя разрешения. Допустимые сопоставления разрешений на защищаемые объекты описаны далее в подразделе «Примечания».  
  
 НА ПОЛНОТЕКСТОВЫЙ КАТАЛОГ **::***full text_catalog_name*  
 Указывает полнотекстовый каталог, на который отменяется разрешение. Квалификатор области **::** является обязательным.  
  
 НА ПОЛНОТЕКСТОВЫЙ список стоп-СЛОВ **::***full text_stoplist_name*  
 Указывает список полнотекстовых стоп-слов, на который отменяется разрешение. Квалификатор области **::** является обязательным.  
  
 *database_principal*  
 Задает участника, у которого отменяется разрешение. Это может быть:  
  
-   пользователь базы данных;  
  
-   роль базы данных;  
  
-   роль приложения;  
  
-   пользователь базы данных, сопоставленный с именем входа Windows;  
  
-   пользователь базы данных, сопоставленный с группой Windows;  
  
-   пользователь базы данных, сопоставленный с сертификатом;  
  
-   пользователь базы данных, сопоставленный асимметричному ключу;  
  
-   пользователь базы данных, не сопоставленный участнику [системы безопасности] на уровне сервера.  
  
 CASCADE  
 Указывает, что отозванное разрешение отзывается также у других участников, которым оно было предоставлено этим участником.  
  
> [!CAUTION]  
>  Каскадная отмена разрешения, предоставленного с помощью параметра WITH GRANT OPTION, приведет к отмене разрешений GRANT и DENY для этого разрешения.  
  
 AS *revoking_principal*  
 Указывает участника, от которого участник, выполняющий данный запрос, получает право на отмену разрешения. Это может быть:  
  
-   пользователь базы данных;  
  
-   роль базы данных;  
  
-   роль приложения;  
  
-   пользователь базы данных, сопоставленный с именем входа Windows;  
  
-   пользователь базы данных, сопоставленный с группой Windows;  
  
-   пользователь базы данных, сопоставленный с сертификатом;  
  
-   пользователь базы данных, сопоставленный асимметричному ключу;  
  
-   пользователь базы данных, не сопоставленный участнику [системы безопасности] на уровне сервера.  
  
## <a name="remarks"></a>Замечания  
  
## <a name="fulltext-catalog-permissions"></a>Разрешения FULLTEXT CATALOG  
 Полнотекстовый каталог представляет собой защищаемый объект уровня базы данных, содержащийся в той базе данных, которая является его родителем в иерархии разрешений. Наиболее специфичные и ограниченные разрешения, которые можно отменять для полнотекстового каталога, перечислены в следующей таблице вместе с более общими разрешениями, неявно их содержащими.  
  
|Разрешение на полнотекстовый каталог|Содержится в разрешении полнотекстового каталога|Содержится в разрешении базы данных|  
|-----------------------------------|----------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY FULLTEXT CATALOG|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="fulltext-stoplist-permissions"></a>Разрешения FULLTEXT STOPLIST  
 Список полнотекстовых стоп-слов является защищаемым объектом уровня базы данных, содержащимся в базе данных, являющейся его родительским элементом в иерархии разрешений. Наиболее специфичные и ограниченные разрешения, которые можно отменять на список полнотекстовых стоп-слов, перечислены в следующей таблице вместе с более общими разрешениями, неявно их содержащими.  
  
|Разрешение на список полнотекстовых стоп-слов|Содержится в разрешении на список полнотекстовых стоп-слов|Содержится в разрешении базы данных|  
|------------------------------------|-----------------------------------------------|------------------------------------|  
|ALTER|CONTROL|ALTER ANY FULLTEXT CATALOG|  
|CONTROL|CONTROL|CONTROL|  
|REFERENCES|CONTROL|REFERENCES|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Permissions  
 Необходимо разрешение CONTROL на полнотекстовый каталог.  
  
## <a name="see-also"></a>См. также:  
 [СОЗДАТЬ РОЛЬ приложения &#40; Transact-SQL &#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [CREATE CERTIFICATE (Transact-SQL)](../../t-sql/statements/create-certificate-transact-sql.md)   
 [CREATE FULLTEXT CATALOG #40; Transact-SQL &#41;](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)   
 [СОЗДАТЬ ПОЛНОТЕКСТОВЫЙ список стоп-СЛОВ &#40; Transact-SQL &#41;](../../t-sql/statements/create-fulltext-stoplist-transact-sql.md)   
 [Иерархия средств шифрования](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [sys.fn_my_permissions &#40; Transact-SQL &#41;](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md)   
 [Разрешения GRANT Full-Text &#40; Transact-SQL &#41;](../../t-sql/statements/grant-full-text-permissions-transact-sql.md)   
 [HAS_PERMS_BY_NAME (Transact-SQL)](../../t-sql/functions/has-perms-by-name-transact-sql.md)   
 [Разрешения (компонент Database Engine)](../../relational-databases/security/permissions-database-engine.md)   
 [Участники (компонент Database Engine)](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [REVOKE (Transact-SQL)](../../t-sql/statements/revoke-transact-sql.md)   
 [sys.fn_builtin_permissions (Transact-SQL)](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)   
 [sys.fulltext_catalogs &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md)   
 [sys.fulltext_stoplists (Transact-SQL)](../../relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql.md)  
  
  
