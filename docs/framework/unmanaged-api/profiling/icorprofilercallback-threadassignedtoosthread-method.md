---
title: Metodo ICorProfilerCallback::ThreadAssignedToOSThread
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorProfilerCallback.ThreadAssignedToOSThread
api_location: mscorwks.dll
api_type: COM
f1_keywords: ICorProfilerCallback::ThreadAssignedToOSThread
helpviewer_keywords:
- ThreadAssignedToOSThread method [.NET Framework profiling]
- ICorProfilerCallback::ThreadAssignedToOSThread method [.NET Framework profiling]
ms.assetid: f9671e5a-7b14-4f5b-8404-58136422c8b2
topic_type: apiref
caps.latest.revision: "12"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 42c23a8190ea611d0333ebd96a31428574191b23
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/22/2017
---
# <a name="icorprofilercallbackthreadassignedtoosthread-method"></a>Metodo ICorProfilerCallback::ThreadAssignedToOSThread
Notifica al profiler che un thread gestito viene implementato utilizzando un thread del sistema operativo in uso.  
  
## <a name="syntax"></a>Sintassi  
  
```  
HRESULT ThreadAssignedToOSThread(  
    [in] ThreadID managedThreadId,  
    [in] DWORD    osThreadId);  
```  
  
#### <a name="parameters"></a>Parametri  
 `managedThreadId`  
 [in] L'identificatore del thread gestito.  
  
 `osThreadId`  
 [in] Identificatore del thread del sistema operativo.  
  
## <a name="remarks"></a>Note  
 Il `ThreadAssignedToOSThread` richiamata in modo che il profiler può mantenere un mapping accurato tra i fiber thread del sistema operativo e i thread gestiti.  
  
## <a name="requirements"></a>Requisiti  
 **Piattaforme:** vedere [requisiti di sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Intestazione:** CorProf.idl, CorProf.h  
  
 **Libreria:** CorGuids.lib  
  
 **Versioni di .NET framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Interfaccia ICorProfilerCallback](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)
