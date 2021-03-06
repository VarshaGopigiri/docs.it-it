---
title: Enumerazione RUNTIME_INFO_FLAGS
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: RUNTIME_INFO_FLAGS
api_location: mscoree.dll
api_type: COM
f1_keywords: RUNTIME_INFO_FLAGS
helpviewer_keywords: RUNTIME_INFO_FLAGS enumeration [.NET Framework hosting]
ms.assetid: adba37be-f775-4cdb-8919-5746ce694f33
topic_type: apiref
caps.latest.revision: "14"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: d050972857ba652ae0b40727260f681c383208b0
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/22/2017
---
# <a name="runtimeinfoflags-enumeration"></a>Enumerazione RUNTIME_INFO_FLAGS
Contiene valori che indicano le informazioni su common language runtime (CLR) devono essere restituite.  
  
## <a name="syntax"></a>Sintassi  
  
```  
typedef enum {  
  
    RUNTIME_INFO_UPGRADE_VERSION             = 0x01,  
    RUNTIME_INFO_REQUEST_IA64                = 0x02,  
    RUNTIME_INFO_REQUEST_AMD64               = 0x04,  
    RUNTIME_INFO_REQUEST_X86                 = 0x08,  
    RUNTIME_INFO_DONT_RETURN_DIRECTORY       = 0x10,  
    RUNTIME_INFO_DONT_RETURN_VERSION         = 0x20,  
    RUNTIME_INFO_DONT_SHOW_ERROR_DIALOG      = 0x40,  
    RUNTIME_INFO_IGNORE_ERROR_MODE           = 0x1000  
  
} RUNTIME_INFO_FLAGS;  
```  
  
## <a name="members"></a>Membri  
  
|Membro|Descrizione|  
|------------|-----------------|  
|`RUNTIME_INFO_DONT_RETURN_DIRECTORY`|Indica che non devono essere incluse informazioni di directory.|  
|`RUNTIME_INFO_DONT_RETURN_VERSION`|Indica che non devono essere incluse informazioni sulla versione.|  
|`RUNTIME_INFO_DONT_SHOW_ERROR_DIALOG`|Indica che non deve essere visualizzata una finestra di dialogo di errore in caso di errore.|  
|`RUNTIME_INFO_IGNORE_ERROR_MODE`|Indica che gli effetti della chiamata di [SetErrorMode](http://go.microsoft.com/fwlink/p/?LinkId=255242) funzione con il flag SEM_FAILCRITICALERRORS deve essere sottoposto a override. Vale a dire la finestra di dialogo installazione deve essere visualizzata in caso di errore, anziché da eliminare.|  
|`RUNTIME_INFO_REQUEST_AMD64`|Indica una richiesta di informazioni su una versione AMD-64 compatibile del runtime.|  
|`RUNTIME_INFO_REQUEST_IA64`|Indica una richiesta di informazioni su una versione IA-64 compatibile del runtime.|  
|`RUNTIME_INFO_REQUEST_X86`|Indica una richiesta di informazioni su una versione x86 compatibile di runtime.|  
|`RUNTIME_INFO_UPGRADE_VERSION`|Indica che devono essere incluse informazioni di aggiornamento di versione.|  
  
## <a name="remarks"></a>Note  
 I flag dell'architettura di piattaforma seguenti possono essere specificati solo uno alla volta e non possono essere combinati:  
  
-   RUNTIME_INFO_REQUEST_IA64  
  
-   RUNTIME_INFO_REQUEST_AMD64  
  
-   RUNTIME_INFO_REQUEST_X86  
  
## <a name="requirements"></a>Requisiti  
 **Piattaforme:** vedere [requisiti di sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Intestazione:** Mscoree. H  
  
 **Libreria:** MSCorEE.dll  
  
 **Versioni di .NET framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Enumerazioni di hosting](../../../../docs/framework/unmanaged-api/hosting/hosting-enumerations.md)
