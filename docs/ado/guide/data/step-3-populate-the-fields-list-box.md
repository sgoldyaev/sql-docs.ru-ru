---
title: "Шаг 3: Заполнения списка полей | Документы Microsoft"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 315c32dc-aeb1-4629-b30e-87b44e8f84d1
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6ef92cbf72ad8a8aa3a8076be7ccaf3761f51ab0
ms.contentlocale: ru-ru
ms.lasthandoff: 09/09/2017

---
# <a name="step-3-populate-the-fields-list-box"></a>Шаг 3: Заполнения списка полей
Для заполнения списка полей, вставьте следующий код в обработчик событий нажатия `lstMain`:  
  
```  
Private Sub lstMain_Click()  
    Dim rec As Record  
    Dim rs As Recordset  
    Set rec = New Record  
    Set rs = New Recordset  
    grs.MoveFirst  
    grs.Move lstMain.ListIndex  
    lstDetails.Clear  
    rec.Open grs  
    Select Case rec.RecordType  
        Case adCollectionRecord:  
            Set rs = rec.GetChildren  
            While Not rs.EOF  
                lstDetails.AddItem rs(0)  
                rs.MoveNext  
            Wend  
        Case adSimpleRecord:  
            recFields rec, lstDetails, txtDetails  
  
        Case adStructDoc:  
    End Select  
  
End Sub  
```  
  
 Этот код объявляет и создает локальные объекты набора записей и записи, `rec` и `rs`соответственно.  
  
 Строка, соответствующая ресурсов, выбранных в `lstMain` становится текущей строке `grs`. Затем снят список сведений и `rec` открывается с текущей строке `grs` как источник.  
  
 Если ресурс является записи коллекции, в соответствии с [RecordType](../../../ado/reference/ado-api/recordtype-property-ado.md), локальный набор записей `rs` открывается на дочерние элементы rec. Затем `lstDetails` заполняется значениями из строки `rs`.  
  
 Если ресурс является запись простой `recFields` вызывается. Дополнительные сведения о `recFields`, см. следующий шаг.  
  
 Код не реализуется в том случае, если ресурс структурированный документ.  
  
## <a name="see-also"></a>См. также:  
 [Сценарий публикации в Интернете](../../../ado/guide/data/internet-publishing-scenario.md)   
 [Шаг 2: Инициализируйте главном списке](../../../ado/guide/data/step-2-initialize-the-main-list-box.md)   
 [Шаг 4: Заполнить текстовое поле сведений](../../../ado/guide/data/step-4-populate-the-details-text-box.md)