---
title: Enumerazione CorSerializationType
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: CorSerializationType
api_location: mscoree.dll
api_type: COM
f1_keywords: CorSerializationType
helpviewer_keywords: CorSerializationType enumeration [.NET Framework metadata]
ms.assetid: 6b1fcd11-c7fb-4be2-8910-abc862d4caf4
topic_type: apiref
caps.latest.revision: "8"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: e43151b1611f5b9b8218d30ba46a9143f463c193
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/22/2017
---
# <a name="corserializationtype-enumeration"></a>Enumerazione CorSerializationType
Specifica come un oggetto viene serializzato da common language runtime.  
  
## <a name="syntax"></a>Sintassi  
  
```  
typedef enum CorSerializationType {  
  
    SERIALIZATION_TYPE_UNDEFINED     = 0,  
    SERIALIZATION_TYPE_BOOLEAN       = ELEMENT_TYPE_BOOLEAN,  
    SERIALIZATION_TYPE_CHAR          = ELEMENT_TYPE_CHAR,  
    SERIALIZATION_TYPE_I1            = ELEMENT_TYPE_I1,  
    SERIALIZATION_TYPE_U1            = ELEMENT_TYPE_U1,  
    SERIALIZATION_TYPE_I2            = ELEMENT_TYPE_I2,  
    SERIALIZATION_TYPE_U2            = ELEMENT_TYPE_U2,  
    SERIALIZATION_TYPE_I4            = ELEMENT_TYPE_I4,  
    SERIALIZATION_TYPE_U4            = ELEMENT_TYPE_U4,  
    SERIALIZATION_TYPE_I8            = ELEMENT_TYPE_I8,  
    SERIALIZATION_TYPE_U8            = ELEMENT_TYPE_U8,  
    SERIALIZATION_TYPE_R4            = ELEMENT_TYPE_R4,  
    SERIALIZATION_TYPE_R8            = ELEMENT_TYPE_R8,  
    SERIALIZATION_TYPE_STRING        = ELEMENT_TYPE_STRING,  
    SERIALIZATION_TYPE_SZARRAY       = ELEMENT_TYPE_SZARRAY,  
    SERIALIZATION_TYPE_TYPE          = 0x50,  
    SERIALIZATION_TYPE_TAGGED_OBJECT = 0x51,  
    SERIALIZATION_TYPE_FIELD         = 0x53,  
    SERIALIZATION_TYPE_PROPERTY      = 0x54,  
    SERIALIZATION_TYPE_ENUM          = 0x55  
  
} CorSerializationType;  
```  
  
## <a name="members"></a>Membri  
  
|Membro|Descrizione|  
|------------|-----------------|  
|`SERIALIZATION_TYPE_UNDEFINED`|Serializzazione dell'oggetto è definita.|  
|`SERIALIZATION_TYPE_BOOLEAN`|L'oggetto è serializzato come tipo booleano.|  
|`SERIALIZATION_TYPE_CHAR`|Oggetto viene serializzato come tipo di carattere.|  
|`SERIALIZATION_TYPE_I1`|Oggetto viene serializzato come un intero con segno a 1 byte.|  
|`SERIALIZATION_TYPE_U1`|Oggetto viene serializzato come un intero senza segno a 1 byte.|  
|`SERIALIZATION_TYPE_I2`|Oggetto viene serializzato come un intero con segno a 2 byte.|  
|`SERIALIZATION_TYPE_U2`|Oggetto viene serializzato come un intero senza segno a 2 byte.|  
|`SERIALIZATION_TYPE_I4`|Oggetto viene serializzato come un intero con segno a 4 byte.|  
|`SERIALIZATION_TYPE_U4`|Oggetto viene serializzato come un intero senza segno a 4 byte.|  
|`SERIALIZATION_TYPE_I8`|Oggetto viene serializzato come un intero con segno a 8 byte.|  
|`SERIALIZATION_TYPE_U8`|Oggetto viene serializzato come un intero senza segno a 8 byte.|  
|`SERIALIZATION_TYPE_R4`|Oggetto viene serializzato come un punto a virgola mobile a 4 byte.|  
|`SERIALIZATION_TYPE_R8`|Oggetto viene serializzato come un punto a virgola mobile a 8 byte.|  
|`SERIALIZATION_TYPE_STRING`|Oggetto viene serializzato come tipo System. String.|  
|`SERIALIZATION_TYPE_SZARRAY`|L'oggetto viene serializzato come unidimensionale, matrice di limite inferiore zero.|  
|`SERIALIZATION_TYPE_TYPE`|Oggetto viene serializzato come tipo generico.|  
|`SERIALIZATION_TYPE_TAGGED_OBJECT`|Oggetto viene serializzato come oggetto con tag.|  
|`SERIALIZATION_TYPE_FIELD`|Oggetto viene serializzato come un campo.|  
|`SERIALIZATION_TYPE_PROPERTY`|Oggetto viene serializzato come proprietà.|  
|`SERIALIZATION_TYPE_ENUM`|Oggetto viene serializzato come un'enumerazione.|  
  
## <a name="requirements"></a>Requisiti  
 **Piattaforme:** vedere [requisiti di sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Intestazione:** CorHdr. H  
  
 **Versioni di .NET framework:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Enumerazioni dei metadati](../../../../docs/framework/unmanaged-api/metadata/metadata-enumerations.md)
