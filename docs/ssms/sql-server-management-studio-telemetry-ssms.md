---
title: Среда SQL Server Management Studio. Телеметрия (SSMS) | Документация Майкрософт
ms.custom: ''
ms.date: 02/20/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: c28ffa44-7b8b-4efa-b755-c7a3b1c11ce4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: abe3642cf4d74b67fcb595548a498fb062d5cddd
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/01/2018
ms.locfileid: "47633352"
---
# <a name="local-audit-for-ssms-usage-feedback-collection"></a>Локальный аудит для сбора отзывов об использовании SSMS
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Среда SQL Server Management Studio (SSMS) содержит функции, работающие через Интернет, с помощью которых можно собирать и отправлять в корпорацию Майкрософт анонимные данные об использовании компонентов. SSMS может собирать стандартные сведения о компьютере, а также сведения об использовании и производительности. Эти данные могут отправляться в корпорацию Майкрософт и использоваться для анализа в целях улучшения качества, безопасности и надежности среды SSMS. Сбор таких сведений, как имена, адреса и другие сведения личного характера, не осуществляется. Дополнительные сведения см. на странице о [конфиденциальности и файлах cookie](http://go.microsoft.com/fwlink/?LinkID=868444).

## <a name="audit-feature-usage-data"></a>Данные об использовании компонентов для аудита

Чтобы просмотреть данные об использовании компонентов, собранные SSMS, сделайте следующее:
1.  Запустите среду SSMS.
2.  Щелкните **Просмотр**, а затем выберите в главном меню **Вывод**, чтобы отобразить окно **вывода**. 
3.  Когда появится окно **Вывод**, выберите в меню **Показать выходные данные из:** пункт **Телеметрия**.

Если вы используете SSMS для взаимодействия с базами данных, в окне **Вывод** отображаются собранные данные.

## <a name="enable-or-disable-usage-feedback-collection-in-ssms"></a>Включение и отключение в среде SSMS сбора информации об использовании

Вы можете согласиться на сбор данных об использовании среды SSMS или отказаться от него. Дополнительные сведения см. в статье [Как настроить 2016 SQL Server для отправки отзывов в корпорацию Майкрософт](http://support.microsoft.com/help/3153756/how-to-configure-sql-server-2016-to-send-feedback-to-microsoft).

## <a name="see-also"></a>См. также раздел

[Локальный аудит для сбора отзывов об использовании SQL Server](http://msdn.microsoft.com/library/mt743085.aspx)
