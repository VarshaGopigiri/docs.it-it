---
title: Utilizzo dei componenti serviti con la Global Assembly Cache
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-bcl
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- assemblies [.NET Framework], global assembly cache
- GAC (global assembly cache), serviced components
- serviced components, global assembly cache
- global assembly cache, serviced components
ms.assetid: 3423e5d9-234c-4571-8161-e35f6d130128
caps.latest.revision: "8"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: fb9bd85797dd129f6f34992c58c9772668ce2cb0
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/22/2017
---
# <a name="using-serviced-components-with-the-global-assembly-cache"></a>Utilizzo dei componenti serviti con la Global Assembly Cache
È consigliabile inserire nella Global Assembly Cache i componenti serviti (componenti COM+ di codice gestito). In alcuni scenari, ma non in tutti, la gestione dei componenti serviti non inclusi nella Global Assembly Cache può essere eseguita da Common Language Runtime e dai servizi COM+. Questo caso viene illustrato negli scenari seguenti:  
  
-   Per quanto riguarda i componenti serviti di un'applicazione COM+ Server, è necessario che l'assembly contenente i componenti si trovi nella Global Assembly Cache, poiché Dllhost.exe non viene eseguito nella stessa directory in cui si trovano i componenti serviti.  
  
-   Per quanto riguarda i componenti serviti di un'applicazione COM+ Library, Common Language Runtime e i servizi COM+ sono in grado di risolvere i riferimenti all'assembly contenente i componenti effettuando una ricerca nella directory corrente. In questo caso non è quindi necessario che l'assembly si trovi nella Global Assembly Cache.  
  
-   La situazione è diversa per i componenti serviti di un'applicazione ASP.NET. Se si inserisce l'assembly contenente i componenti serviti nella directory bin in cui risiede il codice base dell'applicazione e si usa la registrazione su richiesta, verrà effettuata la copia con shadowing dell'assembly nella Download Cache, poiché ASP.NET si avvale delle funzionalità di shadowing di Common Language Runtime.  
  
## <a name="see-also"></a>Vedere anche  
 [Uso di assembly e della Global Assembly Cache](../../../docs/framework/app-domains/working-with-assemblies-and-the-gac.md)  
 [Gacutil.exe (strumento Global Assembly Cache)](../../../docs/framework/tools/gacutil-exe-gac-tool.md)
