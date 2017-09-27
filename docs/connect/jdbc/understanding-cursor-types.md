---
title: "Основные сведения о типах курсоров | Документы Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4f4d3db7-4f76-450d-ab63-141237a4f034
caps.latest.revision: 51
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a65c11a0f6c623162049661a11cbc392a3d8b178
ms.contentlocale: ru-ru
ms.lasthandoff: 09/09/2017

---
# <a name="understanding-cursor-types"></a>Основные сведения о типах курсоров
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Операции в реляционной базе данных выполняются над множеством строк. Набор строк, возвращаемый инструкцией SELECT, содержит все строки, которые удовлетворяют условиям, указанным в предложении WHERE инструкции. Такой полный набор строк, возвращаемых инструкцией, называется результирующим набором. Приложения не всегда могут эффективно работать с результирующим набором, представляющим единое целое. Им нужен механизм, позволяющий обрабатывать одну строку или небольшое их число за один раз. Курсоры являются расширением результирующих наборов, которые предоставляют такой механизм.  
  
 Курсоры расширяют возможности обработки результирующего набора, выполняя следующие функции:  
  
-   позиционируясь на отдельные строки результирующего набора;  
  
-   получая одну или несколько строк от текущей позиции в результирующем наборе;  
  
-   поддерживая изменение данных в строке, находящейся в текущей позиции в результирующем наборе;  
  
-   поддерживая разные уровни видимости изменений, сделанных другими пользователями для данных, представленных в результирующем наборе;  
  
> [!NOTE]  
>  Полное описание [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] типов курсоров см. в разделе «Типы курсоров (компонент Database Engine)» в [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] электронной документации.  
  
 Спецификация JDBC обеспечивает поддержку однопроходных курсоров и прокручиваемых курсоров, которые могут учитывать или не учитывать изменения, выполненные другими заданиями, а также быть доступными только для чтения или допускать обновление. Эта функциональность обеспечивается [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) класса.  
  
## <a name="remarks"></a>Замечания  
 Драйвер JDBC поддерживает следующие типы курсоров.  
  
|Результирующий набор<br /><br /> результирующего набора|Тип курсора SQL Server|Характеристики|select<br /><br /> Метод|Буферизация<br /><br /> ответов|Description|  
|------------------------------------|----------------------------|---------------------|-----------------------|----------------------------|-----------------|  
|TYPE_FORWARD_ONLY (CONCUR_READ_ONLY)|Недоступно|Однонаправленный, только для чтения|direct|переполненные|Приложение выполняет один (однонаправленный) проход по результирующему набору. Этот режим активен по умолчанию и действует аналогично курсору TYPE_SS_DIRECT_FORWARD_ONLY. Драйвер считывает весь результирующий набор с сервера в память во время выполнения инструкции.|  
|TYPE_FORWARD_ONLY (CONCUR_READ_ONLY)|Недоступно|Однонаправленный, только для чтения|direct|adaptive|Приложение выполняет один (однонаправленный) проход по результирующему набору. Работает аналогично курсору TYPE_SS_DIRECT_FORWARD_ONLY. Драйвер считывает строки с сервера по мере того как приложение запрашивает строки. Это позволяет снизить загрузку памяти на стороне клиента.|  
|TYPE_FORWARD_ONLY (CONCUR_READ_ONLY)|Быстрый однопроходный|Однонаправленный, только для чтения|курсор|Недоступно|Приложение должно выполнить один (однонаправленный) проход по результирующему набору, используя серверный курсор. Работает аналогично курсору TYPE_SS_SERVER_CURSOR_FORWARD_ONLY.<br /><br /> Строки извлекаются с сервера блоками, размер которых определяется размером выборки.|  
|TYPE_FORWARD_ONLY (CONCUR_UPDATABLE)|Динамический (однопроходный)|Однопроходный, обновляемый|Недоступно|Недоступно|Приложение должно выполнить один (однонаправленный) проход по результирующему набору, чтобы обновить одну или несколько строк.<br /><br /> Строки извлекаются с сервера блоками, размер которых определяется размером выборки.<br /><br /> По умолчанию размер выборки фиксируется, когда приложение вызывает [setFetchSize](../../connect/jdbc/reference/setfetchsize-method-sqlserverresultset.md) метод [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) объекта.<br /><br /> **Примечание:** драйвер JDBC предоставляет функцию адаптивной буферизации, которая позволяет получать результаты выполнения инструкции из [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] как приложение должно их, а не все сразу. Например, если приложение должно получить данные, которые не могут полностью разместиться в памяти приложения, адаптивная буферизация позволяет клиентскому приложению получать значения в виде потока. По умолчанию драйвера "**адаптивный**». Тем не менее, чтобы включить адаптивную буферизацию для однопроходных обновляемых результирующих наборов, приложение должно явно вызвать [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) метод [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) объекта предоставляя **строка** значение «**адаптивной»**. Образец кода см. в разделе [обновление большой образец данных](../../connect/jdbc/updating-large-data-sample.md).|  
|TYPE_SCROLL_INSENSITIVE|Статические|Прокручиваемый, без поддержки обновления.<br /><br /> Внешние операции обновления, вставки и удаления строк не видимы.|Недоступно|Недоступно|Приложению требуется моментальный снимок базы данных. Результирующий набор не поддерживает обновление. Поддерживается только CONCUR_READ_ONLY.  Все остальные типы параллелизмы в случае использования с этим типом курсора вызывают исключение.<br /><br /> Строки извлекаются с сервера блоками, размер которых определяется размером выборки.|  
|TYPE_SCROLL_SENSITIVE<br /><br /> (CONCUR_READ_ONLY)|Keyset|Прокручиваемый, только для чтения. Внешние обновления строки являются видимыми, а операции удаления отображаются как отсутствующие данные.<br /><br /> Внешние операции вставки невидимы.|Недоступно|Недоступно|Приложению должны быть видимы только измененные данные для существующих строк.<br /><br /> Строки извлекаются с сервера блоками, размер которых определяется размером выборки.|  
|TYPE_SCROLL_SENSITIVE<br /><br /> (CONCUR_UPDATABLE, CONCUR_SS_SCROLL_LOCKS, CONCUR_SS_OPTIMISTIC_CC, CONCUR_SS_OPTIMISTIC_CCVAL)|Keyset|Прокручиваемый, обновляемый.<br /><br /> Внешние и внутренние обновления строки являются видимыми, а операции удаления отображаются как отсутствующие данные; операции вставки невидимы.|Недоступно|Недоступно|Приложение может изменять данные в существующих строках с помощью объекта ResultSet. Приложения также должны быть видимы увидеть изменения в строках, выполненные другими пользователями вне объекта ResultSet.<br /><br /> Строки извлекаются с сервера блоками, размер которых определяется размером выборки.|  
|TYPE_SS_DIRECT_FORWARD_ONLY|Недоступно|Однонаправленный, только для чтения|Недоступно|Полная или адаптивная|Целое значение = 2003. Предоставляет клиентский курсор, доступный только для чтения, с полной буферизацией. Серверный курсор не создается.<br /><br /> Поддерживается только тип параллелизма CONCUR_READ_ONLY. Все остальные типы параллелизмы в случае использования с этим типом курсора вызывают исключение.|  
|TYPE_SS_SERVER_CURSOR_FORWARD_ONLY|Быстрый однопроходный|Однонаправленный|Недоступно|Недоступно|Целое значение = 2004. Быстрый режим, доступ ко всем данным выполняется с помощью серверного курсора. В случае использования с типом параллелизма CONCUR_UPDATABLE возможно обновление.<br /><br /> Строки извлекаются с сервера блоками, размер которых определяется размером выборки.<br /><br /> Чтобы включить адаптивную буферизацию в этом случае, приложение должно явно вызвать [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) метод [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) , предоставив **строки ** значение «**адаптивной»**. Образец кода см. в разделе [обновление большой образец данных](../../connect/jdbc/updating-large-data-sample.md).|  
|TYPE_SS_SCROLL_STATIC|Статические|Не отражает обновления, выполненные другими пользователями.|Недоступно|Недоступно|Целое значение = 1004. Приложению требуется моментальный снимок базы данных. Это [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]-синоним для типа JDBC TYPE_SCROLL_INSENSITIVE и имеет одинаковые параметры параллелизма по умолчанию.<br /><br /> Строки извлекаются с сервера блоками, размер которых определяется размером выборки.|  
|TYPE_SS_SCROLL_KEYSET<br /><br /> (CONCUR_READ_ONLY)|Keyset|Прокручиваемый, только для чтения. Внешние обновления строки являются видимыми, а операции удаления отображаются как отсутствующие данные.<br /><br /> Внешние операции вставки невидимы.|Недоступно|Недоступно|Целое значение = 1005. Приложению должны быть видимы только измененные данные для существующих строк. Это [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]-синоним для типа JDBC TYPE_SCROLL_SENSITIVE и имеет одинаковые параметры параллелизма по умолчанию.<br /><br /> Строки извлекаются с сервера блоками, размер которых определяется размером выборки.|  
|TYPE_SS_SCROLL_KEYSET<br /><br /> (CONCUR_UPDATABLE, CONCUR_SS_SCROLL_LOCKS, CONCUR_SS_OPTIMISTIC_CC, CONCUR_SS_OPTIMISTIC_CCVAL)|Keyset|Прокручиваемый, обновляемый.<br /><br /> Внешние и внутренние обновления строки являются видимыми, а операции удаления отображаются как отсутствующие данные; операции вставки невидимы.|Недоступно|Недоступно|Целое значение = 1005. Приложение должно изменять данные, или для него должны быть видимыми измененные данные для существующих строк. Это [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]-синоним для типа JDBC TYPE_SCROLL_SENSITIVE и имеет одинаковые параметры параллелизма по умолчанию.<br /><br /> Строки извлекаются с сервера блоками, размер которых определяется размером выборки.|  
|TYPE_SS_SCROLL_DYNAMIC<br /><br /> (CONCUR_READ_ONLY)|Динамический|Прокручиваемый, только для чтения.<br /><br /> Внешние операции обновления и вставки строк являются видимыми, а операции удаления представляются как временно отсутствующие данные в текущем буфере выборки.|Недоступно|Недоступно|Целое значение = 1006. Приложению должны быть видимы измененные данные для существующих строк, а также вставленные и обновленные строки за время существования курсора.<br /><br /> Строки извлекаются с сервера блоками, размер которых определяется размером выборки.|  
|TYPE_SS_SCROLL_DYNAMIC<br /><br /> (CONCUR_UPDATABLE, CONCUR_SS_SCROLL_LOCKS, CONCUR_SS_OPTIMISTIC_CC, CONCUR_SS_OPTIMISTIC_CCVAL)|Динамический|Прокручиваемый, обновляемый.<br /><br /> Внешние и внутренние операции обновления и вставки строк являются видимыми, а операции удаления представляются как временно отсутствующие данные в текущем буфере выборки.|Недоступно|Недоступно|Целое значение = 1006. Приложение может изменить данные для существующих строк, или вставки или удаления строк с помощью объекта ResultSet. Приложения также должны быть видимы увидеть изменения, вставки и удаления, выполненные другими пользователями вне объекта ResultSet.<br /><br /> Строки извлекаются с сервера блоками, размер которых определяется размером выборки.|  
  
## <a name="cursor-positioning"></a>Позиционирование курсоров  
 Курсоры TYPE_FORWARD_ONLY, TYPE_SS_DIRECT_FORWARD_ONLY и TYPE_SS_SERVER_CURSOR_FORWARD_ONLY поддерживают только [Далее](../../connect/jdbc/reference/next-method-sqlserverresultset.md) метод позиционирования.  
  
 Курсор TYPE_SS_SCROLL_DYNAMIC не поддерживает [абсолютный](../../connect/jdbc/reference/absolute-method-sqlserverresultset.md) и [getRow](../../connect/jdbc/reference/getrow-method-sqlserverresultset.md) методы. Метод absolute можно приблизительно заменить сочетанием вызова [первый](../../connect/jdbc/reference/first-method-sqlserverresultset.md) и [относительный](../../connect/jdbc/reference/relative-method-sqlserverresultset.md) методы для динамических курсоров.  
  
 Метод getRow поддерживается только курсорами TYPE_FORWARD_ONLY, TYPE_SS_DIRECT_FORWARD_ONLY, TYPE_SS_SERVER_CURSOR_FORWARD_ONLY, TYPE_SS_SCROLL_KEYSET и TYPE_SS_SCROLL_STATIC. Метод getRow со всеми типами однонаправленного курсора возвращает количество строк, считанных в курсоре на данный момент.  
  
> [!NOTE]  
>  Если приложение выполняет неподдерживаемый позиционирования или неподдерживаемый вызов метода getRow курсора, создается исключение с сообщением, «запрошенная операция не поддерживается с этим типом курсора.»  
  
 Доступ к удаленным строкам предоставляется только курсорами TYPE_SS_SCROLL_KEYSET и эквивалентными курсорами TYPE_SCROLL_SENSITIVE. Если курсор находится в удаленной строке, значения столбцов недоступны и [rowDeleted](../../connect/jdbc/reference/rowdeleted-method-sqlserverresultset.md) метод возвращает значение «true». Вызовы для получения\<типа > методы исключение с сообщением, «Не удается получить значение из удаленной строки». Удаленные строки нельзя обновлять. Если попытаться вызвать обновление\<типа > метод на удаленную строку, возникает исключение с сообщением, «не удается обновить удаленную строку». Курсор TYPE_SS_SCROLL_DYNAMIC работает аналогичным образом, пока не выходит за пределы текущего буфера выборки.  
  
 Однопроходные и динамические курсоры предоставляют доступ к удаленным строкам аналогичным образом, но только при условии, что курсоры остаются доступными в буфере выборки. Для однопроходных курсоров это реализуется довольно очевидным образом. Для динамических курсоров ситуация усложняется в случае, когда размер выборки превышает 1. Приложение может перемещать курсор в обоих направлениях в пределах окна, заданного буфером выборки, однако удаленная строка будет исчезать, когда курсор будет покидать исходный буфер выборки, в котором была обновлена строка. Если временно удаленные строки не должны отображаться приложению, использующему динамические курсоры, следует использовать относительную выборку (0).  
  
 Если значения ключа для строки курсора TYPE_SS_SCROLL_KEYSET или TYPE_SCROLL_SENSITIVE обновляются с помощью курсора, то строка сохраняет исходную позицию в результирующем наборе независимо от того, отвечает ли обновленная строка условиям выборки курсора. Если строка обновляется вне курсора, то удаленная строка будет выводиться в исходной позиции строки, однако будет видна в курсоре только в случае, если в курсоре ранее присутствовала другая строка с новыми значениями ключа, однако затем была удалена.  
  
 Для динамических курсоров обновленные строки будут сохранять свои позиции в буфере выборки, пока курсор не покинет окно, определенное буфером выборки. Обновленные строки могут вновь появляться в других позициях в результирующем наборе или полностью исчезать. Приложения, которые должны избегать временной потери согласованности в результирующем наборе, должны использовать размер выборки 1 (по умолчанию используется 8 строк для параллелизма CONCUR_SS_SCROLL_LOCKS и 128 строк для остальных режимов параллелизма).  
  
## <a name="cursor-conversion"></a>Преобразование курсоров  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Иногда выбирает реализацию типа курсора, отличный от запрошенного, который называется неявным преобразованием курсора (или ухудшением курсора). Дополнительные сведения о неявном преобразовании курсора см. в разделе «Использование неявных преобразований курсора» в [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] электронной документации.  
  
 С [!INCLUDE[ssVersion2000](../../includes/ssversion2000_md.md)], при обновлении данных по результирующему ResultSet.TYPE_SCROLL_SENSITIVE и ResultSet.CONCUR_UPDATABLE задано, создается исключение с сообщение «курсора только для чтения». Это исключение возникает, поскольку [!INCLUDE[ssVersion2000](../../includes/ssversion2000_md.md)] выполнил неявное преобразование курсора, для этого результирующего набора и не вернул обновляемый курсор, который был запрошен.  
  
 Для этой проблемы существует два возможных решения.  
  
-   Убедитесь, что базовая таблица содержит первичный ключ.  
  
-   Используйте [SQLServerResultSet.TYPE_SS_SCROLL_DYNAMIC](../../connect/jdbc/reference/type-ss-scroll-dynamic-field-sqlserverresultset.md) вместо ResultSet.TYPE_SCROLL_SENSITIVE создания инструкции.  
  
## <a name="cursor-updating"></a>Обновление курсоров  
 Обновления на месте поддерживаются для курсоров, если тип курсора и тип параллелизма поддерживают обновления. Если курсор не располагается в обновляемой строке в результирующем наборе (не get\<типа > успешного вызова метода), вызов обновления\<типа > метод будет вызывать исключение с сообщением, «результирующий набор не содержит текущую строку.» В спецификации JDBC утверждается, что если метод обновления вызывается для столбца курсора, имеющего тип CONCUR_READ_ONLY, то создается исключение. В ситуациях, когда строка не обновления, например из-за конфликта оптимистичного параллелизма, например в случае конкурирующих операций обновления или удаления, исключение может не создаваться до [insertRow](../../connect/jdbc/reference/insertrow-method-sqlserverresultset.md), [updateRow](../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md), или [deleteRow](../../connect/jdbc/reference/deleterow-method-sqlserverresultset.md) вызывается.  
  
 После вызова метода для обновления\<тип >, столбцу будет невозможен с помощью get\<типа > до updateRow или [cancelRowUpdates](../../connect/jdbc/reference/cancelrowupdates-method-sqlserverresultset.md) был вызван. Это позволяет избежать проблем, когда столбец обновляется с использованием типа, который отличается от типа, возвращенного сервером, а последующие вызовы метода считывания могут привести к преобразованиям типа на клиентской стороне, которые дают неточные результаты. Вызовы для получения\<типа > будет вызвано исключение с сообщением, «обновляемым столбцам невозможен до вызова метода updateRow() или cancelRowUpdates() был вызван.»  
  
> [!NOTE]  
>  Если метод updateRow вызывается, когда столбцы не обновлены, драйвер JDBC вызовет исключение с сообщением, «метод updateRow() вызван, когда столбцы не обновлены.»  
  
 После [moveToInsertRow](../../connect/jdbc/reference/movetoinsertrow-method-sqlserverresultset.md) был вызван, будет создано исключение при любой метод, отличный от получения\<тип >, обновить\<тип >, insertRow и методов позиционирования курсора (включая [ moveToCurrentRow](../../connect/jdbc/reference/movetocurrentrow-method-sqlserverresultset.md)) вызываются в результирующем наборе. Метод moveToInsertRow фактически переводит результирующий набор в режим вставки, а методы позиционирования курсора отменяют режим вставки. Вызовы относительного позиционирования курсора перемещают курсор относительно позиции, в которой он находился перед moveToInsertRow был вызван. После вызова позиционирования курсора ожидаемая позиция назначения становится новой позицией курсора.  
  
 Если вызов позиционирования курсора, выполненный в инструкции insert режиме не завершается успешно, позиция курсора после ошибки вызова будет Исходная позиция курсора до moveToInsetRow был вызван. Если происходит сбой insertRow, то курсор остается в строке вставки и курсор остается в режиме вставки.  
  
 Столбцы в строке вставке первоначально находятся в неинициализированном состоянии. Вызовы к обновлению\<типа > метод присвоено состояние столбца инициализирована. Вызов get\<типа > метода для неинициализированного столбца возникло исключение. Вызов метода insertRow возвращает все столбцы в строке вставки в неинициализированное состояние.  
  
 Если какие-либо столбцы не инициализированы, когда вызывается метод insertRow, вставляется значение по умолчанию для столбца. Если значение по умолчанию отсутствует, но столбец допускает значение NULL, то вставляется значение NULL. Если отсутствует значение по умолчанию, и столбец не допускает значения NULL, то сервер возвращает ошибку, и создается исключение.  
  
> [!NOTE]  
>  Вызовы метода getRow возвращает 0 в режиме вставки.  
>   
>  Драйвер JDBC не поддерживает позиционированные операции обновления и удаления. В соответствии со спецификацией JDBC [setCursorName](../../connect/jdbc/reference/setcursorname-method-sqlserverstatement.md) метод не оказывает влияния и [getCursorName](../../connect/jdbc/reference/getcursorname-method-sqlserverresultset.md) метод будет вызывать исключение при вызове.  
>   
>  Статические курсоры и курсоры, доступные только для чтения, никогда не поддерживают обновление.  
>   
>  SQL Server ограничивает использование серверных курсоров единственным результирующим набором. Если пакет или хранимая процедура содержит несколько инструкций, то необходимо использовать клиентский однопроходный курсор, доступный только для чтения.  
  
## <a name="see-also"></a>См. также:  
 [Управление результирующими наборами с драйвером JDBC](../../connect/jdbc/managing-result-sets-with-the-jdbc-driver.md)  
  
  