---
title: Funzione EnumerateCLRs
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: EnumerateCLRs
api_location: dbgshim.dll
api_type: COM
f1_keywords: EnumerateCLRs
helpviewer_keywords:
- debugging API [Silverlight]
- Silverlight, debugging
- EnumerateCLRs function
ms.assetid: f8d50cb3-ec4f-4529-8fe3-bd61fd28e13c
topic_type: apiref
caps.latest.revision: "4"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 6539b471d6a3075bb4cec69b382cf7702a439d5a
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/22/2017
---
# <a name="enumerateclrs-function"></a>Funzione EnumerateCLRs
Fornisce un meccanismo per l'enumerazione di CLR in un processo.  
  
## <a name="syntax"></a>Sintassi  
  
```  
HRESULT EnumerateCLRs (  
    [in]  DWORD      debuggeePID,  
    [out] HANDLE**   ppHandleArrayOut,  
    [out] LPWSTR**   ppStringArrayOut,  
    [out] DWORD*     pdwArrayLengthOut  
);  
```  
  
#### <a name="parameters"></a>Parametri  
 `debuggeePID`  
 [in] Identificatore del processo da cui verranno enumerati i CLR caricati.  
  
 `ppHandleArrayOut`  
 [out] Puntatore a una matrice contenente handle di evento usati per continuare un avvio di CLR. Non è garantito che ogni handle nella matrice sia valido. Se valido, l'handle deve essere usato come evento di avvio-continuazione per il rispettivo runtime presente nello stesso indice di `ppStringArrayOut`.  
  
 `ppStringArrayOut`  
 [out] Puntatore a una matrice di stringhe che specificano i percorsi completi di CLR caricati nel processo.  
  
 `pdwArrayLengthOut`  
 [out] Puntatore a un valore DWORD che contiene la lunghezza di `ppHandleArrayOut` e `pdwArrayLengthOut` con dimensioni identiche.  
  
## <a name="return-value"></a>Valore restituito  
 S_OK  
 Il numero di CLR nel processo è stato determinato correttamente e le matrici di percorsi e di handle corrispondenti sono state riempite correttamente.  
  
 E_INVALIDARG  
 `ppHandleArrayOut` o `ppStringArrayOut` è Null oppure `pdwArrayLengthOut` è Null.  
  
 E_OUTOFMEMORY  
 La funzione non è in grado di allocare memoria sufficiente per le matrici di percorsi e di handle.  
  
 E_FAIL (o altri codici E_ restituiti)  
 Impossibile enumerare i CLR caricati.  
  
## <a name="remarks"></a>Note  
 Per un processo di destinazione identificato da `debuggeePID`, la funzione restituisce una matrice di percorsi (`ppStringArrayOut`) ai CLR caricati nel processo, una matrice di handle di evento (`ppHandleArrayOut`) che può contenere un evento di avvio-continuazione del CLR per lo stesso indice, oltre alle dimensioni delle matrici (`pdwArrayLengthOut`) che specificano il numero di CLR caricati.  
  
 Nel sistema operativo Windows `debuggeePID` esegue il mapping a un identificatore di processo del sistema operativo.  
  
 La memoria per `ppHandleArrayOut` e `ppStringArrayOut` viene allocata da questa funzione. Per liberare la memoria allocata, è necessario chiamare [funzione CloseCLREnumeration](../../../../docs/framework/unmanaged-api/debugging/closeclrenumeration-function.md).  
  
 Questa funzione può essere chiamata con entrambi i parametri di matrice impostati su Null per restituire il conteggio di CLR nel processo di destinazione. Da questo conteggio un chiamante è in grado di dedurre le dimensioni del buffer che verrà creato: `(sizeof(HANDLE) * count) + (sizeof(LPWSTR) * count) + (sizeof(WCHAR*) * count * MAX_PATH)`.  
  
## <a name="requirements"></a>Requisiti  
 **Piattaforme:** vedere [requisiti di sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Intestazione:** dbgshim. h  
  
 **Libreria:** dbgshim.dll  
  
 **Versioni di .NET framework:** 3.5 SP1
