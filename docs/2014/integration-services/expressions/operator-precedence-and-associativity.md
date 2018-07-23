---
title: Очередность и ассоциативность операторов | Документы Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- associativity [Integration Services]
- precedence [Integration Services]
ms.assetid: 5094164f-dabc-45b5-b611-384feb2b3fe3
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1cd491119fb0af27eb9e2692271fe168e630dc98
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2018
ms.locfileid: "37219644"
---
# <a name="operator-precedence-and-associativity"></a>Очередность и ассоциативность операторов
  Каждый оператор в наборе операторов, поддерживаемом средством оценки выражений, имеет назначенный приоритет в иерархии приоритетов и содержит направление, в котором производится его вычисление. Направление вычисления для оператора — это ассоциативность оператора. Операторы с более высоким приоритетом выполняются раньше операторов с более низким приоритетом. Если выполнение выражения предполагает наличие нескольких операторов, порядок выполнения этих операторов определяется их приоритетом. Порядок исполнения может существенно повлиять на результирующее значение. Некоторые операторы имеют одинаковый приоритет. Если выражение содержит несколько операторов с одинаковым приоритетом, то операторы выполняются направленно, слева направо или справа налево.  
  
 В следующей таблице представлен список операторов в порядке убывания приоритета. Операторы одного уровня имеют одинаковый приоритет.  
  
|Символ оператора|Тип операции|Ассоциативность|  
|---------------------|-----------------------|-------------------|  
|( )|Выражение|Слева направо|  
|–, !, ~|Унарный|Справа налево|  
|Приведения|Унарный|Справа налево|  
|*, / ,%|Мультипликативные|Слева направо|  
|+, –|Аддитивная|Слева направо|  
|\<, >, \<=, >=|Отношение|Слева направо|  
|==, !=|Равенство|Слева направо|  
|&|Побитовое И|Слева направо|  
|^|Побитовое исключающее ИЛИ|Слева направо|  
|&#124;|Побитовое ИЛИ|Слева направо|  
|&&|Логическое И|Слева направо|  
|&#124;&#124;|Логическое ИЛИ|Слева направо|  
|? , перечислены ниже.|Условное выражение|Справа налево|  
  
## <a name="see-also"></a>См. также  
 [Операторы &#40;выражение служб SSIS&#41;](operators-ssis-expression.md)  
  
  