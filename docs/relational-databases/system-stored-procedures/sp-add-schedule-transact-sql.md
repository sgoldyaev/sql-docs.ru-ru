---
title: "sp_add_schedule (Transact-SQL) | Документы Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_add_schedule_TSQL
- sp_add_schedule
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_schedule
ms.assetid: 9060aae3-3ddd-40a5-83bb-3ea7ab1ffbd7
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: df04306671a8e2a0f0ded0fc7482e56955102a83
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/03/2018
---
# <a name="spaddschedule-transact-sql"></a>sp_add_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Создает расписание, которое может использоваться любым количеством заданий.  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
sp_add_schedule [ @schedule_name = ] 'schedule_name'   
    [ , [ @enabled = ] enabled ]  
    [ , [ @freq_type = ] freq_type ]  
    [ , [ @freq_interval = ] freq_interval ]   
    [ , [ @freq_subday_type = ] freq_subday_type ]   
    [ , [ @freq_subday_interval = ] freq_subday_interval ]   
    [ , [ @freq_relative_interval = ] freq_relative_interval ]   
    [ , [ @freq_recurrence_factor = ] freq_recurrence_factor ]   
    [ , [ @active_start_date = ] active_start_date ]   
    [ , [ @active_end_date = ] active_end_date ]   
    [ , [ @active_start_time = ] active_start_time ]   
    [ , [ @active_end_time = ] active_end_time ]   
    [ , [ @owner_login_name = ] 'owner_login_name' ]  
    [ , [ @schedule_uid = ] schedule_uid OUTPUT ]  
    [ , [ @schedule_id = ] schedule_id OUTPUT ]  
    [ , [ @originating_server = ] server_name ] /* internal */  
```  
  
## <a name="arguments"></a>Аргументы  
 [ **@schedule_name =** ] **'***schedule_name***'**  
 Имя расписания. *schedule_name*— **sysname**, не имеет значения по умолчанию.  
  
 [  **@enabled =** ] *включена*  
 Отображает текущее состояние расписания. *включить*— **tinyint**, значение по умолчанию **1** (включено). Если **0**, расписание не включено. Когда расписание не включено, никакие задания не будут запускаться по расписанию.  
  
 [ **@freq_type =** ] *freq_type*  
 Значение, указывающее, когда должно выполняться задание. *freq_type*— **int**, значение по умолчанию **0**, и может принимать одно из следующих значений.  
  
|Значение|Описание|  
|-----------|-----------------|  
|**1**|Однократно|  
|**4**|Ежедневно|  
|**8**|Еженедельно|  
|**16**|Ежемесячно|  
|**32**|Ежемесячно, относительно *freq_interval*|  
|**64**|Запустить, когда запускается служба SQLServerAgent|  
|**128**|Запускать, когда компьютер простаивает|  
  
 [ **@freq_interval =** ] *freq_interval*  
 Дни, когда выполняется задание. *freq_interval* — **int**, значение по умолчанию **1**и зависит от значения *freq_type*.  
  
|Значение *freq_type*|Воздействие на *freq_interval*|  
|---------------------------|--------------------------------|  
|**1** (один раз)|*freq_interval* не используется.|  
|**4** (ежедневно)|Каждый *freq_interval* дней.|  
|**8** (еженедельно)|*freq_interval* — один или несколько из следующих (объединены логическим оператором OR):<br /><br /> **1** = воскресенье<br /><br /> **2** = понедельник<br /><br /> **4** = Вторник<br /><br /> **8** = среда<br /><br /> **16** = четверг<br /><br /> **32** = Пятница<br /><br /> **64** = суббота|  
|**16** (ежемесячно)|На *freq_interval* день месяца.|  
|**32** (относительно ежемесячно)|*freq_interval* является одним из следующих:<br /><br /> **1** = воскресенье<br /><br /> **2** = понедельник<br /><br /> **3** = Вторник<br /><br /> **4** = среда<br /><br /> **5** = четверг<br /><br /> **6** = Пятница<br /><br /> **7** = суббота<br /><br /> **8** = Day<br /><br /> **9** = рабочий день<br /><br /> **10** = выходной день|  
|**64** (когда запускается служба SQLServerAgent)|*freq_interval* не используется.|  
|**128**|*freq_interval* не используется.|  
  
 [ **@freq_subday_type =** ] *freq_subday_type*  
 Указывает единицы изменения для *freq_subday_interval*. *freq_subday_type*— **int**, значение по умолчанию **0**, и может принимать одно из следующих значений.  
  
|Значение|Описание (единица измерения)|  
|-----------|--------------------------|  
|**0x1**|В указанное время|  
|**0x2**|Секунды|  
|**0x4**|Минуты|  
|**0x8**|Часы|  
  
 [ **@freq_subday_interval =** ] *freq_subday_interval*  
 Число *freq_subday_type* периодов должно пройти между выполнениями задания. *freq_subday_interval*— **int**, значение по умолчанию **0**. Примечание: Интервал должен быть больше 10 секунд. *freq_subday_interval* учитывается в тех случаях, где *freq_subday_type* равен **1**.  
  
 [ **@freq_relative_interval =** ] *freq_relative_interval*  
 Задание вхождения *freq_interval* в каждом месяце, если *freq_interval* — 32 (ежемесячное относительное расписание). *freq_relative_interval*— **int**, значение по умолчанию **0**, и может принимать одно из следующих значений. *freq_relative_interval* учитывается в тех случаях, где *freq_type* не равно 32.  
  
|Значение|Описание (единица измерения)|  
|-----------|--------------------------|  
|**1**|Первая|  
|**2**|Вторая|  
|**4**|Третья|  
|**8**|Четвертая|  
|**16**|Последняя|  
  
 [ **@freq_recurrence_factor =** ] *freq_recurrence_factor*  
 Число недель или месяцев между запланированными выполнениями задания. *freq_recurrence_factor* используется только в том случае, если *freq_type* — **8**, **16**, или **32**. *freq_recurrence_factor*— **int**, значение по умолчанию **0**.  
  
 [ **@active_start_date =** ] *active_start_date*  
 Дата, когда может начаться выполнение задания. *active_start_date*— **int**, и значение по умолчанию NULL, которое указывает текущую дату. Формат даты: ГГГГMMДД. Если *active_start_date* не равно NULL, дата должна быть больше или равна 19900101.  
  
 После создания расписания проверьте дату начала и убедитесь, что она задана правильно. Дополнительные сведения см в разделе «Планирование даты начала» [Создание и присоединение расписаний к заданиям](http://msdn.microsoft.com/library/079c2984-0052-4a37-a2b8-4ece56e6b6b5).  
  
 При обработке еженедельных или ежемесячных расписаний агент пропускает значение active_start_date, если оно в прошлом, и использует вместо него текущую дату. Когда расписание агента SQL Server создается с использованием хранимой процедуры sp_add_schedule, можно указать параметр active_start_date, который определяет дату начала выполнения задания. Если это еженедельное или ежемесячное расписание, а параметру active_start_date задана дата в прошлом, параметр active_start_date пропускается и в качестве его значения используется текущая дата.  
  
 [ **@active_end_date =** ] *active_end_date*  
 Дата, когда может быть остановлено выполнение задания. *active_end_date*— **int**, значение по умолчанию **99991231**, что означает 31 декабря 9999 года. Используется формат ГГГГММДД.  
  
 [ **@active_start_time =** ] *active_start_time*  
 Время в любой день между *active_start_date* и *active_end_date* для начала выполнения задания. *active_start_time*— **int**, значение по умолчанию **000000**, что означает 12:00:00 по в 24-часовом формате и должно вводиться в формате ЧЧММСС.  
  
 [ **@active_end_time =** ] *active_end_time*  
 Время в любой день между *active_start_date* и *active_end_date* завершения выполнения задания. *active_end_time*— **int**, значение по умолчанию **235959**, что означает 23:59:59. в 24-часовом формате и должно вводиться в формате ЧЧММСС.  
  
 [ **@owner_login_name**= ] **'***owner_login_name***'**  
 Имя сервера-участника, владеющего расписанием. *owner_login_name* — **sysname**, и значение по умолчанию NULL, которое указывает, что расписание будет владеет его создатель.  
  
 [ **@schedule_uid**= ] *schedule_uid***OUTPUT**  
 Уникальный идентификатор для расписания. *schedule_uid* является переменной типа **uniqueidentifier**.  
  
 [ **@schedule_id**= ] *schedule_id***OUTPUT**  
 Идентификатор расписания. *schedule_id* является переменной типа **int**.  
  
 [ **@originating_server**= ] *server_name*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>Значения кода возврата  
 **0** (успешное завершение) или **1** (неуспешное завершение)  
  
## <a name="result-sets"></a>Результирующие наборы  
 Нет  
  
## <a name="remarks"></a>Remarks  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] обеспечивает доступный графический способ управления заданиями и рекомендуется для создания и управления инфраструктурой заданий.  
  
## <a name="permissions"></a>Разрешения  
 По умолчанию эту хранимую процедуру могут выполнять только члены предопределенной роли сервера **sysadmin** . Другим пользователям должна быть предоставлена одна из следующих предопределенных ролей базы данных агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] в базе данных **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Дополнительные сведения о разрешениях этих ролей см. в разделе [Предопределенные роли базы данных агента SQL Server](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
## <a name="examples"></a>Примеры  
  
### <a name="a-creating-a-schedule"></a>A. Создание расписания  
 В следующем примере создается расписание с именем `RunOnce`. Расписание выполняется один раз, в `23:30` в день создания.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_schedule  
    @schedule_name = N'RunOnce',  
    @freq_type = 1,  
    @active_start_time = 233000 ;  
  
GO  
```  
  
### <a name="b-creating-a-schedule-attaching-the-schedule-to-multiple-jobs"></a>Б. Создание расписания, присоединение расписания к нескольким заданиям  
 В следующем примере создается расписание с именем `NightlyJobs`. Задания, использующие это расписание, выполняются на сервере каждый день в `01:00`. В этом примере расписание подключается к заданиям `BackupDatabase` и `RunReports`.  
  
> [!NOTE]  
>  Этот пример предполагает, что задания `BackupDatabase` и `RunReports` уже существуют.  
  
```  
USE msdb ;  
GO  
  
EXEC sp_add_schedule  
    @schedule_name = N'NightlyJobs' ,  
    @freq_type = 4,  
    @freq_interval = 1,  
    @active_start_time = 010000 ;  
GO  
  
EXEC sp_attach_schedule  
   @job_name = N'BackupDatabase',  
   @schedule_name = N'NightlyJobs' ;  
GO  
  
EXEC sp_attach_schedule  
   @job_name = N'RunReports',  
   @schedule_name = N'NightlyJobs' ;  
GO  
```  
  
## <a name="see-also"></a>См. также  
 [Создание и присоединение расписаний к заданиям](http://msdn.microsoft.com/library/079c2984-0052-4a37-a2b8-4ece56e6b6b5)   
 [Планирование задания](http://msdn.microsoft.com/library/f626390a-a3df-4970-b7a7-a0529e4a109c)   
 [Создание расписания](http://msdn.microsoft.com/library/8c7ef3b3-c06d-4a27-802d-ed329dc86ef3)   
 [Агент SQL Server хранимых процедур &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [sp_add_jobschedule &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-add-jobschedule-transact-sql.md)   
 [sp_update_schedule &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-update-schedule-transact-sql.md)   
 [sp_delete_schedule &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [sp_help_schedule &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-schedule-transact-sql.md)   
 [sp_attach_schedule (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)  
  
  