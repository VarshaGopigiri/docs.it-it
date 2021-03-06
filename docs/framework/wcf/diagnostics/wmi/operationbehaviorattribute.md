---
title: OperationBehaviorAttribute
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8c9b0755-9e83-411f-bdcb-61a586022797
caps.latest.revision: "7"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 63824ae2171053bee2af204e748a6fa811f2ba82
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/22/2017
---
# <a name="operationbehaviorattribute"></a>OperationBehaviorAttribute
OperationBehaviorAttribute  
  
## <a name="syntax"></a>Sintassi  
  
```  
class OperationBehaviorAttribute : Behavior  
{  
  boolean AutoDisposeParameters;  
  string Impersonation;  
  string ReleaseInstanceMode;  
  boolean TransactionAutoComplete;  
  boolean TransactionScopeRequired;  
};  
```  
  
## <a name="methods"></a>Metodi  
 La classe OperationBehaviorAttribute non definisce metodi.  
  
## <a name="properties"></a>Proprietà  
 La classe OperationBehaviorAttribute dispone delle proprietà seguenti:  
  
### <a name="autodisposeparameters"></a>AutoDisposeParameters  
 Tipo di dati: booleano  
  
 Tipo di accesso: sola lettura  
  
 Stato della funzionalità di eliminazione automatica per i parametri.  
  
### <a name="impersonation"></a>Rappresentazione  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura  
  
 Indica il livello di rappresentazione del chiamante supportato dall'operazione.  
  
### <a name="releaseinstancemode"></a>ReleaseInstanceMode  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura  
  
 Indica quando riciclare l'oggetto nel corso della chiamata a un'operazione.  
  
### <a name="transactionautocomplete"></a>TransactionAutoComplete  
 Tipo di dati: booleano  
  
 Tipo di accesso: sola lettura  
  
 Indica se eseguire automaticamente il commit della transazione corrente se non si verifica alcuna eccezione non gestita.  
  
### <a name="transactionscoperequired"></a>TransactionScopeRequired  
 Tipo di dati: booleano  
  
 Tipo di accesso: sola lettura  
  
 Indica se l'operazione richiede una transazione.  
  
## <a name="requirements"></a>Requisiti  
  
|MOF|Dichiarato in Servicemodel.mof.|  
|---------|-----------------------------------|  
|Spazio dei nomi|Definito in root\ServiceModel|  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.ServiceModel.OperationBehaviorAttribute>
