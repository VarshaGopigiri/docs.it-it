---
title: Enumerazione CLR_DEBUGGING_PROCESS_FLAGS
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: CLR_DEBUGGING_PROCESS_FLAGS
api_location: mscordbi.dll
api_type: COM
f1_keywords: CLR_DEBUGGING_PROCESS_FLAG
helpviewer_keywords: CLR_DEBUGGING_PROCESS_FLAGS enumeration [.NET Framework debugging]
ms.assetid: 85b85fde-1f87-490b-ba8d-d604670959c3
topic_type: apiref
caps.latest.revision: "19"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 4c6d66f9a11f28ca572e0f1eddc74f3a5197a19d
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/22/2017
---
# <a name="clrdebuggingprocessflags-enumeration"></a>Enumerazione CLR_DEBUGGING_PROCESS_FLAGS
Fornisce i valori utilizzati per il [ICLRDebugging:: OpenVirtualProcess](../../../../docs/framework/unmanaged-api/debugging/iclrdebugging-openvirtualprocess-method.md) metodo.  
  
## <a name="syntax"></a>Sintassi  
  
```  
typedef enum CLR_DEBUGGING_PROCESS_FLAGS  
{  
   CLR_DEBUGGING_MANAGED_EVENT_PENDING = 1,  
   CLR_DEBUGGING_MANAGED_EVENT_DEBUGGER_LAUNCH = 2  
}  CLR_DEBUGGING_PROCESS_FLAGS;  
```  
  
## <a name="members"></a>Membri  
  
|Membro|Descrizione|  
|------------|-----------------|  
|`CLR_DEBUGGING_MANAGED_EVENT_PENDING`|Il runtime dispone di un evento del debugger gestito a non-catch-up per inviare. Vedere la sezione Osservazioni per la distinzione tra gli eventi di aggiornamento e non-catch-up.|  
|`CLR_DEBUGGING_MANAGED_EVENT_DEBUGGER_LAUNCH`|L'evento gestito che è in sospeso è un <xref:System.Diagnostics.Debugger.Launch%2A?displayProperty=nameWithType> richiesta.|  
  
## <a name="remarks"></a>Note  
 Aggiornamento degli eventi includono processo, il dominio applicazione, assembly, modulo e le notifiche di creazione di thread che portano il debugger fino allo stato corrente dopo che è connesso a un processo. Gli eventi non-catch-up, indicati dal `CLR_DEBUGGING_MANAGED_EVENT_PENDING` flag, includere tutte le altri eventi del debugger, ad esempio le eccezioni e le notifiche di assistente al debug gestito.  
  
 Il `CLR_DEBUGGING_MANAGED_EVENT_DEBUGGER_LAUNCH` flag consente al runtime di distinguere tra un'eccezione di terminazione e una richiesta per allegare un debugger gestito che può essere annullato.  
  
## <a name="requirements"></a>Requisiti  
 **Piattaforme:** vedere [requisiti di sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Intestazione:** Metahost. idl, Metahost. h  
  
 **Libreria:** CorGuids.lib  
  
 **Versioni di .NET framework:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Enumerazioni di debug](../../../../docs/framework/unmanaged-api/debugging/debugging-enumerations.md)  
 [Debug](../../../../docs/framework/unmanaged-api/debugging/index.md)
