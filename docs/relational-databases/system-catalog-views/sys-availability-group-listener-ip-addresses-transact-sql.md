---
title: sys.availability_group_listener_ip_addresses (Transact-SQL) | Документация Майкрософт
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- availability_group_listener_ip_addresses
- sys.availability_group_listener_ip_addresses
- availability_group_listener_ip_addresses_TSQL
- sys.availability_group_listener_ip_addresses_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], listeners
- sys.availability_group_listener_ip_addresses catalog view
ms.assetid: e515fa6b-1354-4110-9b70-ab2e6164c992
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ca29b9925de2d2c1c80e18372a8abf6e818edd15
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/01/2018
ms.locfileid: "47814729"
---
# <a name="sysavailabilitygrouplisteneripaddresses-transact-sql"></a>sys.availability_group_listener_ip_addresses (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Возвращает по строке на каждый IP-адрес, который связан с любой Always On прослушивателя группы доступности в кластере сервера отказоустойчивой кластеризации Windows (WSFC).  
  
 Первичный ключ: **listener_id** + **IP-адрес** + **ip_sub_mask**  
  
  
|Имя столбца|Тип данных|Описание|  
|-----------------|---------------|-----------------|  
|**listener_id**|**nvarchar(36)**|GUID ресурса в отказоустойчивой кластеризации Windows Server (WSFC).|  
|**IP-адрес**|**nvarchar(48)**|Настроенный виртуальный IP-адрес прослушивателя группы доступности. Возвращает один адрес IPv4 или IPv6.|  
|**ip_subnet_mask**|**nvarchar(15)**|Настроенная маска подсети IP для адреса IPv4, если он имеется, заданная для прослушивателя группы доступности.<br /><br /> NULL = подсеть IPv6|  
|**is_dhcp**|**bit**|Указывает, настраивается ли IP-адрес по DHCP, одно из следующих значений:<br /><br /> 0 = IP-адрес не настраивается по DHCP.<br /><br /> 1 = IP-адрес настраивается по DHCP.|  
|**network_subnet_ip**|**nvarchar(48)**|IP-адрес подсети, задающий подсеть, к которой принадлежит IP-адрес.|  
|**network_subnet_prefix_length**|**int**|Длина префикса подсети, к которой принадлежит IP-адрес.|  
|**network_subnet_ipv4_mask**|**nvarchar(45)**|Маска подсети, к которой принадлежит IP-адрес. **network_subnet_ipv4_mask** для указания параметров DHCP < network_subnet_option > в предложении WITH DHCP [CREATE AVAILABILITY GROUP](../../t-sql/statements/create-availability-group-transact-sql.md) или [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] инструкции.<br /><br /> NULL = подсеть IPv6|  
|**state**|**tinyint**|Состояние ONLINE/OFFLINE IP-ресурса в кластере WSFC, одно из следующих значений:<br /><br /> 1 = в сети. IP-ресурс находится в режиме «в сети».<br /><br /> 0 = вне сети. IP-ресурс находится вне сети.<br /><br /> 2 = ожидание перехода в режиме «в сети» IP-ресурс находится вне сети, но производится его перевод в режим «в сети».<br /><br /> 3 = ошибка. В процессе перевода IP-ресурса в режим «в сети» произошла ошибка.|  
|**state_desc**|**nvarchar(60)**|Описание **состояние**, используя один из:<br /><br /> ONLINE<br /><br /> OFFLINE<br /><br /> ONLINE_PENDING<br /><br /> FAILED|  
  
## <a name="security"></a>безопасность  
  
### <a name="permissions"></a>Разрешения  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Дополнительные сведения см. в разделе [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>См. также  
 [Запросив системный каталог SQL Server часто задаваемые вопросы](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [Представления каталога (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
