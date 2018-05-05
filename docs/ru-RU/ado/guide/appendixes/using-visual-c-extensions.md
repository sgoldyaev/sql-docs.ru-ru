---
title: Использование расширений Visual C++ | Документы Microsoft
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- Visual C++ [ADO], using VC++ extensions
- ADO, Visual C++
ms.assetid: ff759185-df41-4507-8d12-0921894ffbd9
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cefa64e3677fa1d6c2660d288c59b4ffe79d4e9b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/03/2018
---
# <a name="visual-c-extensions"></a>Расширения Visual C++
## <a name="the-iadorecordbinding-interface"></a>Интерфейс IADORecordBinding
 Расширения Visual C++ Корпорация Майкрософт для полей ADO сопоставить или связать, [записей](../../../ado/reference/ado-api/recordset-object-ado.md) объекта к переменным C/C++. Каждый раз, когда текущей строки границы **записей** изменяет привязанных полей в **записей** копируются на переменные C/C++. При необходимости копируемых данных преобразуется объявленный тип данных переменной C/C++.

 **BindToRecordset** метод **IADORecordBinding** интерфейс привязывает поля на переменные C/C++. **AddNew** метод добавляет новую строку с границей **записей**. **Обновление** метод заполняет поля в новые строки **записей**, или обновляет поля в существующих строках, значения переменных C/C++.

 **IADORecordBinding** интерфейс реализуется **записей** объекта. Не следует кодировать реализации самостоятельно.

## <a name="binding-entries"></a>Элементы привязки
 Расширения Visual C++ для ADO сопоставить поля [записей](../../../ado/reference/ado-api/recordset-object-ado.md) объекта к переменным C/C++. Определение сопоставления между полем и переменной называется *привязки запись*. Макросы предоставляют записи привязки для числовых, фиксированной и переменной длины данных. Элементы привязки и переменных C/C++ объявлены в классе, производном от класса расширения Visual C++, **CADORecordBinding**. **CADORecordBinding** внутри определения класса в записи макросов привязки.

 ADO внутренне сопоставляется параметры в этих макросов OLE DB **DBBINDING** структуры и создает OLE DB **доступа** объект для управления перемещения и преобразования данных между полями и переменные. OLE DB определяет данные, как состоящий из трех частей: A *буфера* там, где хранятся данные; *состояние* указывает ли поле было успешно сохранены в буфере или как должен быть восстановлен переменной поле; и *длина* данных. (См. [начало и параметр данных (OLE DB)](http://msdn.microsoft.com/en-us/4369708b-c9fb-4d48-a321-bf949b41a369)в справочнике программиста OLE DB.)

## <a name="header-file"></a>Файл заголовка
 В приложении для использования расширений Visual C++ для ADO, добавьте следующий файл:

```
#include <icrsint.h>
```

## <a name="binding-recordset-fields"></a>Привязка полей набора записей

#### <a name="to-bind-recordset-fields-to-cc-variables"></a>Для привязки переменных C/C++ полям набора записей

1.  Создайте класс, производный от **CADORecordBinding** класса.

2.  Укажите привязку операции и соответствующие переменные C/C++ в производном классе. Квадратная скобка связям между **BEGIN_ADO_BINDING** и **END_ADO_BINDING** макросы. Не прерывайте макросов с запятой или точкой с запятой. Каждый макрос автоматически задаются соответствующие разделители.

     Укажите одну запись привязки для каждого поля для сопоставления переменной C/C++. Используйте соответствующий элемент из **ADO_FIXED_LENGTH_ENTRY**, **ADO_NUMERIC_ENTRY**, или **ADO_VARIABLE_LENGTH_ENTRY** семейства макросов.

3.  В приложении, создайте экземпляр класса, производного от **CADORecordBinding**. Получить **IADORecordBinding** интерфейс из **записей**. Затем вызовите **BindToRecordset** метод привязки **записей** полей для переменных C/C++.

 Дополнительные сведения см. в разделе [пример расширения Visual C++](../../../ado/guide/appendixes/visual-c-extensions-example.md).

## <a name="interface-methods"></a>Методы интерфейса
 **IADORecordBinding** интерфейса есть три метода: **BindToRecordset**, **AddNew**, и **обновление**. Единственным аргументом каждого метода является указателем на экземпляр класса, производного от **CADORecordBinding**. Таким образом **AddNew** и **обновление** методы нельзя указывать ни один из параметров их namesakes метода ADO.

## <a name="syntax"></a>Синтаксис
 **BindToRecordset** связывает метод **записей** поля с переменными C/C++.

```
BindToRecordset(CADORecordBinding *binding)
```

 **AddNew** метод вызывает его namesake ADO [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) метод, чтобы добавить новую строку в **записей**.

```
AddNew(CADORecordBinding *binding)
```

 **Обновление** метод вызывает его namesake ADO [обновление](../../../ado/reference/ado-api/update-method.md) метод обновления **записей**.

```
Update(CADORecordBinding *binding)
```

## <a name="binding-entry-macros"></a>Макросы записи привязки
 Макросы записи привязки определяют связь **записей** поля и переменной. Начальный и конечный макрос разделяет набор привязки операции.

 Семейства макросов предоставляются для данных фиксированной длины, таких как **adDate** или **adBoolean**; числовых данных, таких как **adTinyInt**, **adInteger**, или **adDouble**; и данные переменной длины, таких как **adChar**, **adVarChar** или **adVarBinary**. Все числовые типы, за исключением **adVarNumeric**, также являются типами фиксированной длины. Каждое семейство имеет различные наборы параметров, можно исключить сведения о привязке, не представляет интереса.

 Дополнительные сведения см. в разделе [типов данных в приложении A:](http://msdn.microsoft.com/en-us/e3a0533a-2196-4eb0-a31e-92fe9556ada6), ссылки на программиста OLE DB.

### <a name="begin-binding-entries"></a>Начать привязки операции
 **BEGIN_ADO_BINDING**(*класса*)

### <a name="fixed-length-data"></a>Данные фиксированной длины
 **ADO_FIXED_LENGTH_ENTRY**(*изменить порядковый номер, тип данных, буфера, состояние,*)

 **ADO_FIXED_LENGTH_ENTRY2**(*изменить порядковый номер, тип данных, буфера,*)

### <a name="numeric-data"></a>Числовые данные
 **ADO_NUMERIC_ENTRY**(*изменить порядковый номер, тип данных, буфера, точность, масштаб, состояние,*)

 **ADO_NUMERIC_ENTRY2**(*изменить порядковый номер, тип данных, буфера, точность, масштаб,*)

### <a name="variable-length-data"></a>Данные переменной длины
 **ADO_VARIABLE_LENGTH_ENTRY**(*порядковый номер, тип данных, буфер, размер, состояние, длину, измените*)

 **ADO_VARIABLE_LENGTH_ENTRY2**(*изменить порядковый номер, тип данных, буфер, размер, состояние,*)

 **ADO_VARIABLE_LENGTH_ENTRY3**(*порядковый номер, тип данных, буфер, размер, длину, измените*)

 **ADO_VARIABLE_LENGTH_ENTRY4**(*изменить порядковый номер, тип данных, буфер, размер,*)

### <a name="end-binding-entries"></a>Привязка операции End
 **END_ADO_BINDING**()

|Параметр|Описание|
|---------------|-----------------|
|*Class*|Класс определенные элементы привязки и переменных C/C++.|
|*Ordinal*|Порядковый номер, начиная с единицы, из **записей** поле, соответствующее вашей переменной C/C++.|
|*Тип данных*|Эквивалентным типом данных ADO переменной C/C++ (в разделе [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) список допустимых типов данных). Значение **записей** поля будут преобразованы в этот тип данных, при необходимости.|
|*Буфер*|Имя переменной C/C++ где **записей** поля будут храниться.|
|*Размер*|Максимальный размер в байтах *буфера*. Если *буфера* будет содержать строку переменной длины, пространство для завершающего нуля.|
|*Состояние*|Имя переменной, которая будет указывать ли содержимое *буфера* являются допустимыми и необходимость преобразования поля для *DataType* прошла успешно.<br /><br /> Два наиболее важные значения для этой переменной **adFldOK**, означающее преобразование выполнено успешно; и **adFldNull**, что означает, что значение поля может быть РАЗНОВИДНОСТЬЮ VT_NULL и не просто пустой.<br /><br /> Возможные значения параметра *состояние* , перечислены в следующей таблице, «Состояние значения».|
|*Изменение*|Логический флаг; значение TRUE указывает, ADO может обновлять соответствующие **записей** поле значение, содержащееся в *буфера*.<br /><br /> Значение типа Boolean *изменить* параметр в значение TRUE, чтобы позволить ADO обновить связанные поля и значение FALSE, если вы хотите проверить это поле, но не изменять.|
|*Точность*|Число знаков, которые могут быть представлены в числовой переменной.|
|*Масштаб*|Число десятичных разрядов в числовой переменной.|
|*Длина*|Имя переменной 4 байта, в которой будет содержать фактическую длину данных в *буфера*.|

## <a name="status-values"></a>Индикаторы состояния
 Значение *состояние* переменная указывает, является ли поле успешно скопирована в переменной.

 При вводе данных, *состояние* может быть задано значение **adFldNull** для указания **записей** должно быть задано значение null.

|Константа|Значение|Описание|
|--------------|-----------|-----------------|
|**adFldOK**|0|Возвращено значение поля, отличных от null.|
|**adFldBadAccessor**|1|Привязка была недействительной.|
|**adFldCantConvertValue**|2|Не удалось преобразовать значение, по причинам, отличным от несоответствия знака или данные переполнения.|
|**adFldNull**|3|При получении поле, указывает, что возвратил значение null.<br /><br /> При задании поля, указывает поле должно быть присвоено **NULL** когда поле не может закодировать **NULL** себе (например, массив символов или целое число).|
|**adFldTruncated**|4|Данные переменной длины или цифрам было усечено.|
|**adFldSignMismatch**|5|Подписанные значение и тип данных переменной без знака.|
|**adFldDataOverFlow**|6|Значение больше, чем может храниться в тип данных переменной.|
|**adFldCantCreate**|7|Неизвестный тип столбца и поле уже открыт.|
|**adFldUnavailable**|8|Не удалось определить значение поля, например, на новое поле неназначенные без значения по умолчанию.|
|**adFldPermissionDenied**|9|При обновлении, отсутствует разрешение на запись данных.|
|**adFldIntegrityViolation**|10|При обновлении, значение поля приведет к нарушению целостности для столбца.|
|**adFldSchemaViolation**|11|При обновлении, значение поля приведет к нарушению столбца схемы.|
|**adFldBadStatus**|12|При обновлении параметра недопустимое состояние.|
|**adFldDefault**|13|При обновлении, было использовано значение по умолчанию.|

## <a name="see-also"></a>См. также
 [Пример расширения Visual C++](../../../ado/guide/appendixes/visual-c-extensions-example.md) [заголовок расширений Visual C++](../../../ado/guide/appendixes/visual-c-extensions-header.md)