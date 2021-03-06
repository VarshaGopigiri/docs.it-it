---
title: Interfaccia ICorDebugManagedCallback2
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorDebugManagedCallback2
api_location: mscordbi.dll
api_type: COM
f1_keywords: ICorDebugManagedCallback2
helpviewer_keywords: ICorDebugManagedCallback2 interface [.NET Framework debugging]
ms.assetid: cf7b7cfa-1c4b-4d8c-be70-4f9ed15a788b
topic_type: apiref
caps.latest.revision: "13"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 2a46e8e4f23c57391877d8cb6ba6b35d50de151b
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/22/2017
---
# <a name="icordebugmanagedcallback2-interface"></a>Interfaccia ICorDebugManagedCallback2
Fornisce metodi che supportano la gestione delle eccezioni del debugger e assistenti al debug gestito. `ICorDebugManagedCallback2`è un'estensione logica del [ICorDebugManagedCallback](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback-interface.md) interfaccia.  
  
## <a name="methods"></a>Metodi  
  
|Metodo|Descrizione|  
|------------|-----------------|  
|[Metodo ChangeConnection](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback2-changeconnection-method.md)|Notifica al debugger che il set di attività associata alla connessione specificata è stato modificato.|  
|[Metodo CreateConnection](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback2-createconnection-method.md)|Notifica al debugger che è stata creata una nuova connessione.|  
|[Metodo DestroyConnection](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback2-destroyconnection-method.md)|Notifica al debugger che la connessione specificata è stata terminata.|  
|[Metodo Exception](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback2-exception-method.md)|Notifica al debugger che si è iniziata una ricerca di un gestore di eccezioni.|  
|[Metodo ExceptionUnwind](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback2-exceptionunwind-method.md)|Fornisce una notifica sullo stato durante il processo di rimozione di eccezione.|  
|[Metodo FunctionRemapComplete](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback2-functionremapcomplete-method.md)|Notifica al debugger che l'esecuzione di codice è passata a una nuova versione di una funzione modificata.|  
|[Metodo FunctionRemapOpportunity](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback2-functionremapopportunity-method.md)|Notifica al debugger che l'esecuzione del codice ha raggiunto un punto di sequenza in una versione precedente di una funzione modificata.|  
|[Metodo MDANotification](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback2-mdanotification-method.md)|Fornisce una notifica che l'esecuzione del codice ha rilevato un messaggio di assistente al debug gestito.|  
  
## <a name="remarks"></a>Note  
 Il `ICorDebugManagedCallback2` interfaccia estende il `ICorDebugManagedCallback` interfaccia per gestire i nuovi eventi di debug introdotti in .NET Framework versione 2.0.  
  
 Un debugger deve implementare `ICorDebugManagedCallback2` se sta eseguendo il debug di applicazioni .NET Framework 2.0. Un'istanza di `ICorDebugManagedCallback` o `ICorDebugManagedCallback2` viene passato come oggetto di callback da [ICorDebug:: SetManagedHandler](../../../../docs/framework/unmanaged-api/debugging/icordebug-setmanagedhandler-method.md).  
  
> [!NOTE]
>  Questa interfaccia non supporta la chiamata in modalità remota, tra computer o tra processi.  
  
## <a name="requirements"></a>Requisiti  
 **Piattaforme:** vedere [requisiti di sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Intestazione:** CorDebug.idl, Cordebug. H  
  
 **Libreria:** CorGuids.lib  
  
 **Versioni di .NET framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Diagnostica degli errori tramite gli assistenti al debug gestito](../../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)  
 [Interfacce di debug](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)  
 [Interfaccia ICorDebugManagedCallback](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback-interface.md)
