---
title: 'Создание разделов CDATA с использованием SQL: USE-cdata (SQLXML 4.0) | Документация Майкрософт'
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- markup characters [SQLXML]
- special characters [SQLXML]
- use-cdata annotation
- plain text [SQLXML]
- CDATA sections
- escaping blocks of text [SQLXML]
- annotated XSD schemas, CDATA sections
- sql:use-cdata
ms.assetid: 26d2b9dc-f857-44ff-bcd4-aaf64ff809d0
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 599acd5082d4dcf00d2eab8174fa695cd839032d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/01/2018
ms.locfileid: "47785152"
---
# <a name="creating-cdata-sections-using-sqluse-cdata-sqlxml-40"></a>Создание разделов CDATA с использованием sql:use-cdata (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  В XML разделы CDATA используются для экранирования блоков текста, содержащих символы, которые в противном случае распознаются как символы разметки.  
  
 Иногда в базе данных в Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] могут содержаться символы, которые в средстве синтаксического анализа XML рассматриваются как символы разметки. Например, символами разметки считаются угловые скобки (< и >), символ меньше или равно (<=), а также амперсанд (&). Но специальные символы такого типа можно заключить в раздел CDATA во избежание их обработки в качестве символов разметки. Текст в разделе CDATA обрабатывается средством синтаксического анализа XML как простой текст.  
  
 **SQL: USE-cdata** заметка используется для указания данных, возвращаемых методом [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] должно заключаться в раздел CDATA (то есть он указывает, является ли значение из столбца, заданные **SQL: field** должно быть заключено в раздел CDATA). **SQL: USE-cdata** заметки можно указать только на элементы, сопоставляемые со столбцом базы данных.  
  
 **SQL: USE-cdata** заметка имеет логическое значение (0 = false, 1 = true). Допустимые значения: 0, 1, true и false.  
  
 Эта заметка не может использоваться с **заметки SQL: URL-кодирование** или для ID, IDREF, IDREFS, NMTOKEN и NMTOKENS атрибутов типов.  
  
## <a name="examples"></a>Примеры  
 Чтобы создать рабочие образцы на основе следующих примеров, необходимо выполнить определенные требования. Дополнительные сведения см. в разделе [требования для запуска примеров SQLXML](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-specifying-sqluse-cdata-on-an-element"></a>A. Указание заметки sql:use-cdata для элемента  
 В следующей схеме **SQL: USE-cdata** имеет значение 1 (True) для  **\<AddressLine1 >** в  **\<адрес >** элемент. В результате этого данные возвращаются в разделе CDATA.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Address"   
               sql:relation="Person.Address"   
               sql:key-fields="AddressID" >  
   <xsd:complexType>  
        <xsd:sequence>  
          <xsd:element name="AddressID"  type="xsd:string" />  
          <xsd:element name="AddressLine1" type="xsd:string"   
                       sql:use-cdata="1" />  
        </xsd:sequence>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>Проверка образца запроса XPath к схеме  
  
1.  Скопируйте приведенный выше код схемы и вставьте его в текстовый файл. Сохраните этот файл с именем UseCData.xml.  
  
2.  Скопируйте следующий шаблон и вставьте его в текстовый файл. Сохраните этот файл под именем UseCDataT.xml в том же каталоге, в котором был сохранен файл UseCData.xml.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="UseCData.xml">  
            /Address[AddressID < 11]  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     Путь к каталогу схемы сопоставления (файл UseCData.xml) задается относительно каталога, в котором сохранен шаблон. Можно также задать абсолютный путь, например:  
  
    ```  
    mapping-schema="C:\SqlXmlTest\UseCData.xml"  
    ```  
  
3.  Создайте и запустите тестовый скрипт SQLXML 4.0 (Sqlxml4test.vbs), чтобы выполнить шаблон.  
  
     Дополнительные сведения см. в разделе [использование объектов ADO для выполнения запросов SQLXML 4.0](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Ниже приведен частичный результирующий набор.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">   
  <Address>   
    <AddressID>1</CustomerID>   
    <AddressLine1>   
      <![CDATA[ 1970 Napa Ct.  ]]>   
    </AddressLine1>   
  </Address>  
  <Address>  
    <AddressLine1>   
      <![CDATA[ 9833 Mt. Dias Blv. ]]>   
    </AddressLine1>   
  </Address>  
  ...  
</ROOT>  
```  
  
  
