---
title: Metodo IHostCrst::SetSpinCount
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: IHostCrst.SetSpinCount
api_location: mscoree.dll
api_type: COM
f1_keywords: IHostCrst::SetSpinCount
helpviewer_keywords:
- IHostCrst::SetSpinCount method [.NET Framework hosting]
- SetSpinCount method [.NET Framework hosting]
ms.assetid: 863fc8ce-9b8a-477e-8dd8-75c8544bb43a
topic_type: apiref
caps.latest.revision: "11"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 76a3091102a43d17f543010be0c505157d593d2c
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/22/2017
---
# <a name="ihostcrstsetspincount-method"></a>Metodo IHostCrst::SetSpinCount
Imposta il conteggio di selezione per l'oggetto corrente [IHostCrst](../../../../docs/framework/unmanaged-api/hosting/ihostcrst-interface.md) istanza.  
  
## <a name="syntax"></a>Sintassi  
  
```  
HRESULT SetSpinCount (  
    [in] DWORD dwSpinCount  
);  
```  
  
#### <a name="parameters"></a>Parametri  
 `dwSpinCount`  
 [in] Nuovo numero di selezione per corrente `IHostCrst` istanza.  
  
## <a name="return-value"></a>Valore restituito  
  
|HRESULT|Descrizione|  
|-------------|-----------------|  
|S_OK|`SetSpinCount`stato restituito correttamente.|  
|HOST_E_CLRNOTAVAILABLE|Common language runtime (CLR) non è stato caricato in un processo oppure si trova in uno stato in cui non può eseguire codice gestito o elaborare correttamente la chiamata.|  
|HOST_E_TIMEOUT|Timeout della chiamata.|  
|HOST_E_NOT_OWNER|Il chiamante non dispone del blocco.|  
|HOST_E_ABANDONED|Un evento è stato annullato mentre un thread bloccato o fiber era in attesa su di esso.|  
|E_FAIL|Si è verificato un errore irreversibile sconosciuto. Quando un metodo viene restituito E_FAIL, Common Language Runtime non è più utilizzabile all'interno del processo. Le chiamate successive ai metodi di hosting restituiranno HOST_E_CLRNOTAVAILABLE.|  
  
## <a name="remarks"></a>Note  
 Nei sistemi multiprocessore, se la sezione critica rappresentata dall'oggetto corrente `IHostCrst` istanza non è disponibile, un thread chiamante esegue `dwSpinCount` volte prima di chiamare [IHostSemaphore:: Wait](../../../../docs/framework/unmanaged-api/hosting/ihostsemaphore-wait-method.md) su un semaforo associato con la sezione critica. Se la sezione critica diventa disponibile durante l'operazione di selezione, il thread chiamante evita l'operazione di attesa.  
  
 L'utilizzo di `dwSpinCount` è identico a quello del parametro con lo stesso nome in Win32 `InitializeCriticalSectionAndSpinCount` (funzione).  
  
## <a name="requirements"></a>Requisiti  
 **Piattaforme:** vedere [requisiti di sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Intestazione:** Mscoree. H  
  
 **Libreria:** inclusa come risorsa in MSCorEE.dll  
  
 **Versioni di .NET framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Interfaccia ICLRSyncManager](../../../../docs/framework/unmanaged-api/hosting/iclrsyncmanager-interface.md)  
 [Interfaccia IHostCrst](../../../../docs/framework/unmanaged-api/hosting/ihostcrst-interface.md)  
 [Interfaccia IHostSyncManager](../../../../docs/framework/unmanaged-api/hosting/ihostsyncmanager-interface.md)
