---
title: Передача файлов в папку | Документы Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- publishing reports [Reporting Services], uploading files
- reports [Reporting Services], publishing
- uploading reports [Reporting Services]
- uploading files [Reporting Services]
- files [Reporting Services], uploading
- files [Reporting Services]
- folders [Reporting Services], uploading files to
ms.assetid: 2f99a288-d4aa-4c64-b310-e457a2aef2c5
caps.latest.revision: 41
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: d9abf4ad5aef29b6064b53af80553b02ee01c2fa
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2018
ms.locfileid: "37266150"
---
# <a name="upload-files-to-a-folder"></a>Передача файлов в папку
  Предусмотрена возможность передавать файлы из файловой системы и сохранять их в качестве управляемых элементов в базе данных сервера отчетов. Действия системы при передаче зависят от типа файла.  
  
-   Передача RDL-файла эквивалентна публикации отчета.  
  
-   Передача любого другого файла добавляет его в базу данных сервера отчетов как один двоичный объект. Эти файлы публикуются на сервере отчетов как ресурсы. Ресурсами могут быть файлы любого типа. Если расширение файла совпадает с известным типом MIME, для идентификации типа ресурса используется значок этого типа MIME. В противном случае ресурс показывает универсальный значок файла.  
  
> [!NOTE]  
>  Нельзя передавать файл источника данных отчета (RDS) для создания общего источника данных. RDS-файл используется только в конструкторе отчетов. Он не может предоставлять содержимое для совместно используемого элемента источника данных, определенного и управляемого с помощью диспетчера отчетов. В качестве альтернативы передачи можно написать скрипт, который создает общий источник данных на основе RDS-файла.  
  
 Максимальный размер файла для передаваемых элементов определяется [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)]. По умолчанию максимальный размер равен 4 мегабайтам (МБ).  
  
 Визуально файлы, передаваемые в базу данных сервера отчетов, представляются в иерархии папок с помощью следующих значков:  
  
 ![Значок "Отчет"](../media/hlp-16doc.gif "Значок \"Отчет\"")  
значок отчета  
  
 ![Значок модели](../media/model-icon.gif "Значок модели")  
значок модели отчета  
  
 ![Значок "Универсальный ресурс"](../media/hlp-16file.gif "Значок \"Универсальный ресурс\"")  
универсальный значок ресурса  
  
 При передаче файл всегда помещается в текущую выбранную папку. Можно либо сразу перейти в папку, куда следует сохранить файл, либо передать файл и затем переместить его в нужное место.  
  
 Файл передается с помощью диспетчера отчетов. Возможность передачи файлов на сервер отчетов зависит от задач, которые входят в назначенную роль. Если используются настройки безопасности по умолчанию, локальные администраторы могут добавлять элементы в сервер отчетов. Если включены «Мои отчеты», любой пользователь, для которого создана папка «Мои отчеты», имеет разрешения на передачу в нее элементов. Если используются пользовательские назначения ролей, то назначение роли должно включать задачи, поддерживающие управление папками.  
  
|Чтобы выполнить следующее действие|Необходимо включить следующие задачи|  
|----------------|-------------------------|  
|Передача RDL-файла в папку|Управление отчетами|  
|Передача любого файла как двоичного объекта|Управление ресурсами|  
|Просмотр содержимого папки|Просмотр ресурсов, просмотр отчетов|  
  
## <a name="see-also"></a>См. также  
 [Диспетчер отчетов &#40;собственный режим служб SSRS&#41;]... / отчетов manager-ssrs-машинный код mode.md)   
 [Предоставление разрешений на сервер отчетов в собственном режиме](../security/granting-permissions-on-a-native-mode-report-server.md)   
 [Задачи и разрешения](../security/tasks-and-permissions.md)   
 [Передача файла или отчета (диспетчер отчетов)](../reports/upload-a-file-or-report-report-manager.md)  
  
  