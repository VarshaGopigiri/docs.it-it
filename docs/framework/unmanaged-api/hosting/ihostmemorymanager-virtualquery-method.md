---
title: Metodo IHostMemoryManager::VirtualQuery
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: IHostMemoryManager.VirtualQuery
api_location: mscoree.dll
api_type: COM
f1_keywords: IHostMemoryManager::VirtualQuery
helpviewer_keywords:
- IHostMemoryManager::VirtualQuery method [.NET Framework hosting]
- VirtualQuery method [.NET Framework hosting]
ms.assetid: 757af1e6-b9e8-49e7-b5db-342be3aa205f
topic_type: apiref
caps.latest.revision: "11"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 4fd893cd92f7e7621aefe59595cfd9905bc77afd
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/22/2017
---
# <a name="ihostmemorymanagervirtualquery-method"></a>Metodo IHostMemoryManager::VirtualQuery
Funge da wrapper logico per la funzione Win32 corrispondente. L'implementazione Win32 di `VirtualQuery` recupera informazioni su un intervallo di pagine nello spazio degli indirizzi virtuali del processo chiamante.  
  
## <a name="syntax"></a>Sintassi  
  
```  
HRESULT VirtualQuery (  
    [in]  void*    lpAddress,  
    [out] void*    lpBuffer,  
    [in]  SIZE_T   dwLength,  
    [out] SIZE_T*  pResult  
);  
```  
  
#### <a name="parameters"></a>Parametri  
 `lpAddress`  
 [in] Un puntatore all'indirizzo nella memoria virtuale per eseguire una query.  
  
 `lpBuffer`  
 [out] Puntatore a una struttura che contiene informazioni sull'area di memoria specificata.  
  
 `dwLength`  
 [in] Le dimensioni, in byte, del buffer che `lpBuffer` punta a.  
  
 `pResult`  
 [out] Puntatore al numero di byte restituiti dal buffer delle informazioni.  
  
## <a name="return-value"></a>Valore restituito  
  
|HRESULT|Descrizione|  
|-------------|-----------------|  
|S_OK|`VirtualQuery`stato restituito correttamente.|  
|HOST_E_CLRNOTAVAILABLE|Common language runtime (CLR) non è stato caricato in un processo oppure si trova in uno stato in cui non può eseguire codice gestito o elaborare correttamente la chiamata.|  
|HOST_E_TIMEOUT|Timeout della chiamata.|  
|HOST_E_NOT_OWNER|Il chiamante non dispone del blocco.|  
|HOST_E_ABANDONED|Un evento è stato annullato mentre un thread bloccato o fiber era in attesa su di esso.|  
|E_FAIL|Si è verificato un errore irreversibile sconosciuto. Quando un metodo viene restituito E_FAIL, Common Language Runtime non è più utilizzabile all'interno del processo. Le chiamate successive ai metodi di hosting restituiranno HOST_E_CLRNOTAVAILABLE.|  
  
## <a name="remarks"></a>Note  
 `VirtualQuery`fornisce informazioni su un intervallo di pagine nello spazio degli indirizzi virtuali del processo chiamante. Questa implementazione imposta il valore di `pResult` parametro per il numero di byte restituiti nel buffer di informazioni e restituisce un valore HRESULT. In Win32 `VirtualQuery` funzione, il valore restituito è la dimensione del buffer. Per ulteriori informazioni, vedere la documentazione di piattaforma di Windows.  
  
> [!IMPORTANT]
>  Implementazione del sistema operativo di `VirtualQuery` è soggetta a deadlock e possono eseguire al completamento con thread casuali sospesi nel codice utente. Quando si implementa una versione ospitata di questo metodo, usare estrema cautela.  
  
## <a name="requirements"></a>Requisiti  
 **Piattaforme:** vedere [requisiti di sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Intestazione:** Mscoree. H  
  
 **Libreria:** inclusa come risorsa in MSCorEE.dll  
  
 **Versioni di .NET framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Interfaccia IHostMemoryManager](../../../../docs/framework/unmanaged-api/hosting/ihostmemorymanager-interface.md)
