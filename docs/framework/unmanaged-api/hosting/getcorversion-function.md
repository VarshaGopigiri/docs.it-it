---
title: Funzione GetCORVersion
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: GetCORVersion
api_location:
- mscoree.dll
- mscoreei.dll
api_type: DLLExport
f1_keywords: GetCORVersion
helpviewer_keywords: GetCORVersion function [.NET Framework hosting]
ms.assetid: 2f09cd37-bf3a-4cc5-87b0-adc42a7eed31
topic_type: apiref
caps.latest.revision: "17"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: c61dd0b10bc0229d8f0d7dd4f6357ddaf5986637
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/22/2017
---
# <a name="getcorversion-function"></a>Funzione GetCORVersion
Restituisce il numero di versione di common language runtime (CLR) che è in esecuzione nel processo corrente.  
  
 Questa funzione è stata deprecata nel [!INCLUDE[net_v40_long](../../../../includes/net-v40-long-md.md)].  
  
## <a name="syntax"></a>Sintassi  
  
```  
HRESULT GetCORVersion (  
    [in] LPWSTR  pbuffer,  
    [in]  DWORD   cchBuffer,   
    [out] DWORD*  dwlength  
);   
```  
  
#### <a name="parameters"></a>Parametri  
 `pbuffer`  
 Un puntatore a un buffer in cui CLR restituisce una stringa che specifica la versione del runtime attualmente caricato nel processo. La stringa restituita assume lo stesso formato passata a [CorBindToRuntimeEx](../../../../docs/framework/unmanaged-api/hosting/corbindtoruntimeex-function.md), ad esempio, "v 1.0.1216". Se il runtime non è ancora stato caricato nel processo, la funzione restituisce le informazioni di directory appropriata per la versione più recente del runtime installata nel computer.  
  
 `cchBuffer`  
 Il numero di caratteri (`WCHAR`s) che possono essere contenuti in `pbuffer`.  
  
 `dwLength`  
 Un puntatore al numero di caratteri effettivamente restituiti in `pbuffer`. Se `pbuffer` è un puntatore null, il runtime restituisce E_POINTER. Se il numero di caratteri è maggiore della lunghezza della `pbuffer` , viene restituito ERROR_INSUFFICIENT_BUFFER.  
  
## <a name="requirements"></a>Requisiti  
 **Piattaforme:** vedere [requisiti di sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Intestazione:** Mscoree. H  
  
 **Libreria:** MSCorEE.dll  
  
 **Versioni di .NET framework:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni di hosting CLR deprecate](../../../../docs/framework/unmanaged-api/hosting/deprecated-clr-hosting-functions.md)
