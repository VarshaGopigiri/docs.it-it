---
title: Metodo IMapToken::Map
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: IMapToken.Map
api_location: mscoree.dll
api_type: COM
f1_keywords: IMapToken::Map
helpviewer_keywords:
- IMapToken::Map method [.NET Framework metadata]
- Map method [.NET Framework metadata]
ms.assetid: b9b4bf2f-1098-43d6-9619-a99b4bda1940
topic_type: apiref
caps.latest.revision: "11"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: fe034d2bc6d70e820fa3ad5de8140afa9a19a6bf
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/22/2017
---
# <a name="imaptokenmap-method"></a>Metodo IMapToken::Map
Esegue il mapping di una relazione tra gli assembly che utilizzano le firme di metadati.  
  
## <a name="syntax"></a>Sintassi  
  
```  
HRESULT Map (  
    [in]  mdToken tkImp,   
    [in]  mdToken tkEmit  
);  
```  
  
#### <a name="parameters"></a>Parametri  
 `tkImp`  
 [in] Il token di metadati che rappresenta l'oggetto codice importato.  
  
 `tkEmit`  
 [in] Il token di metadati che rappresenta l'oggetto di codice generato.  
  
## <a name="remarks"></a>Note  
 Quando il nuovo mapping dei token si verifica durante un'operazione di unione, il token originale è un ambito nell'ambito dei metadati importati (origine) e il nuovo token di ambito è nell'ambito dei metadati generato (destinazione).  
  
## <a name="requirements"></a>Requisiti  
 **Piattaforme:** vedere [requisiti di sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Intestazione:** Cor. h  
  
 **Libreria:** usata come risorsa in MsCorEE.dll  
  
 **Versioni di .NET framework:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Interfaccia IMapToken](../../../../docs/framework/unmanaged-api/metadata/imaptoken-interface.md)
