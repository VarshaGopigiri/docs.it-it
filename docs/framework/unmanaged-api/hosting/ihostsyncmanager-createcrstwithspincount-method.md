---
title: Metodo IHostSyncManager::CreateCrstWithSpinCount
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: IHostSyncManager.CreateCrstWithSpinCount
api_location: mscoree.dll
api_type: COM
f1_keywords: IHostSyncManager::CreateCrstWithSpinCount
helpviewer_keywords:
- CreateCrstWithSpinCount method [.NET Framework hosting]
- IHostSyncManager::CreateCrstWithSpinCount method [.NET Framework hosting]
ms.assetid: 7280fa8c-3639-4abf-91cb-bc343da742d1
topic_type: apiref
caps.latest.revision: "11"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 31830f97cff1c302ee573b8248eb1d83e696ac48
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/22/2017
---
# <a name="ihostsyncmanagercreatecrstwithspincount-method"></a>Metodo IHostSyncManager::CreateCrstWithSpinCount
Crea un oggetto sezione critica con conteggio di selezione per la sincronizzazione.  
  
## <a name="syntax"></a>Sintassi  
  
```  
HRESULT CreateCrstWithSpinCount (  
    [in]  DWORD dwSpinCount,  
    [out] IHostCrst** ppCrst  
);  
```  
  
#### <a name="parameters"></a>Parametri  
 `dwSpinCount`  
 [in] Specifica il numero di selezione per l'oggetto sezione critica.  
  
 `ppCrst`  
 [out] Un puntatore all'indirizzo di un [IHostCrst](../../../../docs/framework/unmanaged-api/hosting/ihostcrst-interface.md) oppure null se non è stato possibile creare la sezione critica.  
  
## <a name="return-value"></a>Valore restituito  
  
|HRESULT|Descrizione|  
|-------------|-----------------|  
|S_OK|`CreateCrstWithSpinCount`stato restituito correttamente.|  
|HOST_E_CLRNOTAVAILABLE|Common language runtime (CLR) non è stato caricato in un processo oppure si trova in uno stato in cui non può eseguire codice gestito o elaborare correttamente la chiamata.|  
|HOST_E_TIMEOUT|Timeout della chiamata.|  
|HOST_E_NOT_OWNER|Il chiamante non dispone del blocco.|  
|HOST_E_ABANDONED|Un evento è stato annullato mentre un thread bloccato o fiber era in attesa su di esso.|  
|E_FAIL|Si è verificato un errore irreversibile sconosciuto. Quando un metodo viene restituito E_FAIL, Common Language Runtime non è più utilizzabile all'interno del processo. Le chiamate successive ai metodi di hosting restituiranno HOST_E_CLRNOTAVAILABLE.|  
|E_OUTOFMEMORY|Memoria insufficiente è disponibile per creare la richiesta sezione critica.|  
  
## <a name="remarks"></a>Note  
 Il numero di selezione viene utilizzato solo in un sistema multiprocessore. Il conteggio di selezione specifica il numero di volte in cui che un thread chiamante è necessario attivare prima di eseguire un'operazione di attesa su un semaforo per cui è associata a una sezione critica non disponibile. Se la sezione critica diventa disponibile durante l'operazione di selezione, il thread chiamante evita l'operazione di attesa. `CreateCrstWithSpinCount`rispecchia Win32 `InitializeCriticalSectionAndSpinCount` (funzione).  
  
## <a name="requirements"></a>Requisiti  
 **Piattaforme:** vedere [requisiti di sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Intestazione:** Mscoree. H  
  
 **Libreria:** inclusa come risorsa in MSCorEE.dll  
  
 **Versioni di .NET framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Interfaccia ICLRSyncManager](../../../../docs/framework/unmanaged-api/hosting/iclrsyncmanager-interface.md)  
 [Interfaccia IHostSemaphore](../../../../docs/framework/unmanaged-api/hosting/ihostsemaphore-interface.md)  
 [Interfaccia IHostSyncManager](../../../../docs/framework/unmanaged-api/hosting/ihostsyncmanager-interface.md)
