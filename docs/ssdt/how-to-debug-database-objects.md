---
title: Практическое руководство. Отладка объектов базы данных | Документация Майкрософт
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f5d4584f-e85f-4558-b056-83681c365978
caps.latest.revision: 10
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7379c550b8bcf9ac18b1e7590bad8a10bdc83f3c
ms.sourcegitcommit: 2f07d285824a8982c279f3816b220e61a2d91b06
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/29/2018
ms.locfileid: "37094759"
---
# <a name="how-to-debug-database-objects"></a>Практическое руководство. Отладка объектов базы данных
Модульный тест SQL Server содержит следующие элементы.  
  
-   Код модульного теста на языке Visual Basic или Visual C\#. Этот код, который формируется конструктором модульных тестов SQL Server, отвечает за передачу скрипта Transact\-SQL, составляющего основу теста.  
  
-   Одно или несколько условий теста, написанных на Visual C\# или Visual Basic. Для отладки условий теста следуйте процедуре, описанной в практических руководствах по отладке при выполнении теста [для Visual Studio 2010](http://msdn.microsoft.com/library/ms182484(VS.100).aspx) или [для Visual Studio 2012](http://msdn.microsoft.com/library/ms182484.aspx).  
  
-   Один или несколько скриптов Transact\-SQL, которые работают с объектами в тестируемой базе данных. Вы не можете выполнить отладку этих скриптов Transact\-SQL.  
  
Приведенные в этом разделе инструкции касаются отладки определенных объектов базы данных, например хранимых процедур, функций и триггеров, в тестируемой базе данных. Для выполнения отладки объекта базы данных выполните инструкции в следующем порядке.  
  
1.  Включите отладку SQL Server в тестовом проекте.  
  
2.  Включите отладку приложений в экземпляре SQL Server, в котором размещена тестируемая база данных.  
  
3.  Задайте точки останова в скрипте Transact\-SQL для отлаживаемых объектов базы данных.  
  
4.  Выполните отладку модульного теста. Для этого процесса тест выполняется в режиме отладки.  
  
### <a name="to-enable-sql-debugging-on-your-test-project"></a>Включение отладки SQL в проекте тестов  
  
1.  Откройте **обозреватель решений**.  
  
2.  В **обозревателе решений** щелкните правой кнопкой мыши тестовый проект и выберите **Свойства**.  
  
    Откроется страница свойств с именем проекта тестов.  
  
3.  На странице свойств щелкните **Отладка**.  
  
4.  В разделе **Включение отладчиков** щелкните **Включить отладку SQL Server**.  
  
5.  Сохраните изменения.  
  
### <a name="to-set-an-increased-execution-context-timeout-to-enable-debugging-for-your-test-project"></a>Задание увеличенного времени ожидания контекста выполнения и включение отладки для тестового проекта  
  
1.  В меню **Файл** выберите пункт **Открыть**, а затем щелкните **Файл**.  
  
2.  Перейдите в папку с проектом тестов и дважды щелкните файл app.config.  
  
    Файл app.config откроется в редакторе.  
  
3.  Добавьте в узел ExecutionContext время ожидания команды, как показано в следующем примере.  
  
    ```  
    <ExecutionContext CommandTimeout ="300" Provider="System.Data.SqlClient" ConnectionString="Data Source=TargetServerName\TargetInstanceName;Initial Catalog=TargetDatabaseName;Integrated Security=True;Pooling=False" />  
    ```  
  
4.  Сохраните изменения.  
  
5.  Перестройте проект модульных тестов.  
  
> [!IMPORTANT]  
> Если не перестроить проект, изменения, внесенные в файл app.config, не будут применяться при запуске модульных тестов и отладка будет завершаться ошибкой.  
  
### <a name="to-add-breakpoints-to-your-transact-sql-script"></a>Добавление точек останова в скрипт Transact\-SQL  
  
1.  В меню **Вид** откройте **обозреватель объектов SQL Server**.  
  
2.  На вкладке **Подключение к данным** разверните узел базы данных, которую вы будете тестировать.  
  
3.  Если рядом со значком базы данных находится маленький красный значок «x», соединение с базой данных закрыто. В нашем примере щелкните базу данных правой кнопкой мыши и выберите **Обновить**. Для открытия соединения с базой данных может потребоваться указать учетные данные.  
  
4.  Разверните узел **Представления**, **Хранимые процедуры** или **Функции** и найдите отлаживаемый объект.  
  
5.  Дважды щелкните объект, для которого необходимо выполнить отладку.  
  
6.  Щелкните серую полосу, чтобы установить точку останова.  
  
### <a name="to-debug-your-sql-server-unit-test"></a>Отладка модульного теста SQL Server  
  
1.  В Visual Studio 2010 откройте окно **Представление теста** (Тест -> Окна). В Visual Studio 2012 откройте окно **Обозреватель тестов**.  
  
2.  Щелкните правой кнопкой мыши тест со скриптом Transact\-SQL, работающий с объектом базы данных, в котором установлены точки останова, и выберите **Отладить выбранное**.  
  
    Тест запустится в режиме отладки и будет выполняться до обнаружения точки останова в объекте базы данных.  
  
3.  (Необязательно) Чтобы открыть другое окно отладки, откройте меню **Отладка**, выберите пункт **Окна** и щелкните **Точки останова**, **Вывод** или **Немедленно**.  
  
## <a name="see-also"></a>См. также:  
[Выполнение модульных тестов SQL Server](../ssdt/running-sql-server-unit-tests.md)  
[Отладка Transact-SQL (Visual Studio 2010)](http://go.microsoft.com/fwlink/?LinkId=163975)  
  