---
title: "bcp_colfmt | Документы Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-extensions-bulk-copy-functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: bcp_colfmt
apilocation: sqlncli11.dll
apitype: DLLExport
helpviewer_keywords: bcp_colfmt function
ms.assetid: 5c3b6299-80c7-4e84-8e69-4ff33009548e
caps.latest.revision: "35"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c19dd268f958bc35f6e41fd6a6283ca23beb60e9
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/24/2018
---
# <a name="bcpcolfmt"></a>bcp_colfmt
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Указывает исходный или целевой формат данных в пользовательском файле. При использовании в качестве формате источника **bcp_colfmt** указывает формат существующего файла данных используется в качестве источника данных при массовом копировании для [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] таблицы. При использовании в качестве целевой формат файла данных создается с использованием форматов столбцов, указанных с **bcp_colfmt**.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
RETCODE bcp_colfmt (  
        HDBC hdbc,  
        INT idxUserDataCol,  
        BYTE eUserDataType,  
        INT cbIndicator,  
        DBINT cbUserData,  
        LPCBYTE pUserDataTerm,  
        INT cbUserDataTerm,  
        INT idxServerCol);  
```  
  
## <a name="arguments"></a>Аргументы  
 *HDBC*  
 Дескриптор соединения ODBC с поддержкой массового копирования.  
  
 *idxUserDataCol*  
 Порядковый номер столбца в пользовательском файле данных, для которого указывается формат. Первый столбец имеет номер 1.  
  
 *eUserDataType*  
 Тип данных этого столбца в файле пользователя. Если оно отличается от типа данных соответствующего столбца в таблице базы данных (*idxServerColumn*), массовое копирование преобразует данные, если это возможно.  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]появилась поддержка SQLXML и SQLUDT токенами типов данных в *eUserDataType* параметра.  
  
 *EUserDataType* перечисляется [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] токенами типов данных в файле sqlncli.h, не перечислителях типов данных ODBC C. Например, можно указать символьную строку SQL_C_CHAR типа ODBC с помощью специфического для [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] типа SQLCHARACTER.  
  
 Чтобы задать представление данных по умолчанию для типа данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], установите этот параметр в значение 0.  
  
 Для массового копирования из [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] в файл, когда *eUserDataType* SQLDECIMAL или SQLNUMERIC:  
  
-   Если исходный столбец не **десятичное** или **числовое**, используемые по умолчанию точность и масштаб.  
  
-   Если исходный столбец имеет **десятичное** или **числовое**, используются точность и масштаб исходного столбца.  
  
 *cbIndicator*  
 Длина в байтах признака длины и допустимости значений NULL в данных столбца. Допускаются следующие значения длины признака: 0 (если признак не используется), 1, 2, 4 или 8.  
  
 Чтобы задать для признака массового копирования использование по умолчанию, установите этот параметр в значение SQL_VARLEN_DATA.  
  
 Признаки располагаются в памяти непосредственно перед данными, а в файле данных — непосредственно перед данными, к которым они применяются.  
  
 Если для столбца файла данных используется несколько способов задания длины (например, признак и максимальная длина столбца или признак и последовательность-признак конца), то для массового копирования выбирается способ, применение которого вызовет копирование данных наименьшего объема.  
  
 Если пользователь не изменяет формат данных, то создаваемые при массовом копировании файлы данных содержат признаки, которые определяют, когда столбец может принимать значение NULL или его данные имеют переменную длину.  
  
 *cbUserData*  
 Максимальная длина в байтах данных в столбце пользовательского файла, не включая длину признака длины или признака конца.  
  
 Установка *cbUserData* значение SQL_NULL_DATA означает, что все значения в столбце файла данных, или значение NULL.  
  
 Установка *cbUserData* значения SQL_VARLEN_DATA указывает, что система должна определить длину данных в каждом столбце. Для некоторых столбцов это может означать, что создаваемые признаки длины и допустимости значений NULL предваряют данные при копировании из [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], или ожидается их наличие в данных, копируемых в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Для [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] символьных и двоичных типов данных, *cbUserData* может иметь значение SQL_VARLEN_DATA, SQL_NULL_DATA, 0 или другое положительное значение. Если *cbUserData* имеет значение SQL_VARLEN_DATA, система использует либо признак длины при его наличии, либо признак конца для определения длины данных. Если задан и признак длины, и последовательность признака конца, то при массовом копировании используется значение, применение которого вызывает копирование данных наименьшего объема. Если *cbUserData* имеет значение SQL_VARLEN_DATA, данные типа [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] указан символ или двоичного типа и ни признак длины, ни последовательность признака конца, система возвращает сообщение об ошибке.  
  
 Если *cbUserData* равен 0 или положительное значение, система использует *cbUserData* как максимальную длину данных. Тем не менее если в дополнение к положительному *cbUserData*, указан признак длины или признака конца последовательность, то система определяет объем данных с помощью метода, который вычисляет наименьший размер копируемых данных.  
  
 *CbUserData* значение представляет число байтов данных. Если символьные данные представлены строкой знаков в Юникоде, то положительное *cbUserData* значение параметра представляет число символов, умноженное на размер в байтах каждого символа.  
  
 *pUserDataTerm*  
 Последовательность-признак конца, используемая для этого столбца. Этот параметр предназначен главным образом для символьных типов данных, поскольку все другие типы имеют фиксированную длину или, как в случае с двоичными данными, требуют наличия признака длины, в котором записано точное число присутствующих байтов.  
  
 Чтобы исключить обработку признака конца в извлекаемых данных или указать, что данные в файле пользователя не имеют признака конца, установите этот параметр в значение NULL.  
  
 Если для столбца файла пользователя используется несколько способов задания длины (например, признак конца и признак длины или признак конца и максимальная длина столбца), то для массового копирования выбирается способ, применение которого вызывает копирование данных наименьшего объема.  
  
 При необходимости API-интерфейс массового копирования выполнит преобразование символов из Юникода в многобайтовую кодировку (MBCS). Обратите особое внимание, правильно ли задана строка байтов, служащая признаком конца, а также ее длина.  
  
 *cbUserDataTerm*  
 Длина в байтах последовательности-признака конца, используемой для этого столбца. Если в данных признак конца отсутствует или нежелателен, то установите это значение в 0.  
  
 *idxServerCol*  
 Порядковый номер столбца в таблице базы данных. Первый столбец имеет номер 1. Порядковый номер столбца возвращается функцией [SQLColumns](../../relational-databases/native-client-odbc-api/sqlcolumns.md).  
  
 Если это значение равно 0, операция массового копирования пропускает столбец в файле данных.  
  
## <a name="returns"></a>Возвращает  
 SUCCEED или FAIL.  
  
## <a name="remarks"></a>Remarks  
 **Bcp_colfmt** функция позволяет указать формат пользовательского файла для массового копирования. Формат для массового копирования состоит из следующих частей:  
  
-   сопоставление столбцов файла пользователя со столбцами базы данных;  
  
-   тип данных каждого столбца в файле пользователя;  
  
-   длина дополнительного признака для каждого столбца;  
  
-   максимальная длина данных в каждом столбце файла пользователя;  
  
-   дополнительная последовательность байт, служащая признаком конца для каждого столбца;  
  
-   длина дополнительной последовательности байт, служащей признаком конца.  
  
 Каждый вызов **bcp_colfmt** указывает формат для одного столбца пользовательского файла. Например, чтобы изменить параметры по умолчанию для трех столбцов в файле данных пользователя пять столбцов, сначала вызовите [bcp_columns](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-columns.md)**(5)**, а затем вызвать **bcp_colfmt** пять раз с три из этих вызовов указывая пользовательский формат. Для остальных двух вызовах установите *eUserDataType* равно 0, а также набор *cbIndicator*, *cbUserData*, и *cbUserDataTerm* 0, SQL_VARLEN _DATA и 0 соответственно. Эта процедура копирует все пять столбцов. Для трех применяется заданный измененный формат, а для двух оставшихся — формат по умолчанию.  
  
 Для *cbIndicator*, теперь является допустимым значение 8, указывающее тип больших значений. Если для поля, которому соответствует столбец с новым типом max, указан префикс, его значение можно установить только в 8. Дополнительные сведения см. в разделе [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md).  
  
 **Bcp_columns** функция должна вызываться перед любыми вызовами **bcp_colfmt**.  
  
 Необходимо вызвать **bcp_colfmt** один раз для каждого столбца в файле пользователя.  
  
 Вызов **bcp_colfmt** более одного раза для любой файл пользовательского столбца приводит к ошибке.  
  
 Нет необходимости копировать все данные из пользовательского файла в таблицу [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Чтобы пропустить столбец, укажите формат данных для этого столбца, задав *idxServerCol* в значение 0. Если требуется пропустить столбец, необходимо указать его тип.  
  
 [Bcp_writefmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-writefmt.md) функцию можно использовать для сохранения спецификации формата.  
  
## <a name="bcpcolfmt-support-for-enhanced-date-and-time-features"></a>Поддержка функцией bcp_colfmt улучшенных возможностей даты и времени  
 Дополнительные сведения о типах, используемых с *eUserDataType* параметров для типов даты и времени, в разделе [изменения массового копирования для улучшенной даты и времени типы &#40; OLE DB и ODBC &#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md).  
  
 Дополнительные сведения см. в разделе [даты и времени усовершенствования &#40; ODBC &#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="see-also"></a>См. также  
 [Функции массового копирования](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  