---
title: Funzione CloseCLREnumeration
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: CloseCLREnumeration
api_location: dbgshim.dll
api_type: COM
f1_keywords: CloseCLREnumeration
helpviewer_keywords:
- debugging API [Silverlight]
- Silverlight, debugging
- CloseCLR Enumeration function
ms.assetid: 5e3c3958-80bb-43b1-a96b-dd3e6dbd9cd7
topic_type: apiref
caps.latest.revision: "4"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 2f6de2d1625b4d9f66ec27ad7ed3e6ba33cc59b4
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/22/2017
---
# <a name="closeclrenumeration-function"></a>Funzione CloseCLREnumeration
Chiude qualsiasi valido common language runtime (CLR) continuano l'avvio gli eventi che si trova in una matrice di handle restituita dal [funzione EnumerateCLRs](../../../../docs/framework/unmanaged-api/debugging/enumerateclrs-function.md)e libera la memoria per le matrici del percorso stringa e di handle.  
  
## <a name="syntax"></a>Sintassi  
  
```  
HRESULT CloseCLREnumeration (  
    [in]  DWORD      pHandleArray,  
    [in]  LPWSTR**   pStringArray,  
    [in]  DWORD*     dwArrayLength  
);  
```  
  
#### <a name="parameters"></a>Parametri  
 `pHandleArray`  
 [in] Puntatore alla matrice di handle di evento restituito dal [funzione EnumerateCLRs](../../../../docs/framework/unmanaged-api/debugging/enumerateclrs-function.md).  
  
 `pStringArray`  
 [in] Puntatore alla matrice di percorsi di stringa CLR restituiti dal [funzione EnumerateCLRs](../../../../docs/framework/unmanaged-api/debugging/enumerateclrs-function.md).  
  
 `dwArrayLength`  
 [in] DWORD contenente la dimensione (lunghezza) di `pHandleArray` o `pStringArray` (sono uguali).  
  
## <a name="return-value"></a>Valore restituito  
 S_OK  
 Gli handle aperti per la [funzione EnumerateCLRs](../../../../docs/framework/unmanaged-api/debugging/enumerateclrs-function.md) vengono chiusi, e viene liberata la memoria allocata per le matrici di tipo stringa e di handle.  
  
 E_INVALIDARG  
 La lunghezza di `pHandleArray` non corrisponde alla lunghezza passata in `dwArrayLength`.  
  
 E_FAIL (o altri codici E_ restituiti)  
 La funzione non è in grado di liberare la memoria per `pHandleArray` ed `pStringArray`.  
  
## <a name="requirements"></a>Requisiti  
 **Piattaforme:** vedere [requisiti di sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Intestazione:** dbgshim. h  
  
 **Libreria:** dbgshim.dll  
  
 **Versioni di .NET framework:** 3.5 SP1
