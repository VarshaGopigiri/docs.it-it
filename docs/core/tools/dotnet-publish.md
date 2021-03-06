---
title: Comando dotnet publish - Interfaccia della riga di comando di .NET Core
description: Il comando dotnet publish consente di pubblicare il progetto .NET Core in una directory.
author: mairaw
ms.author: mairaw
ms.date: 09/01/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.workload: dotnetcore
ms.openlocfilehash: e29d5269ab5e9e2c9fd08811552c09ec1c95363d
ms.sourcegitcommit: 3fd4e718d1bac9769fe0c1dd08ca1b2323ae272b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/11/2018
---
# <a name="dotnet-publish"></a>dotnet publish

[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]

## <a name="name"></a>nome

`dotnet publish`: inserisce l'applicazione e le relative dipendenze in una cartella per la distribuzione in un sistema host.

## <a name="synopsis"></a>Riepilogo

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

```
dotnet publish [<PROJECT>] [-c|--configuration] [-f|--framework] [--force] [--manifest] [--no-dependencies] [--no-restore] [-o|--output] [-r|--runtime] [--self-contained] [-v|--verbosity] [--version-suffix]
dotnet publish [-h|--help]
```

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

```
dotnet publish [<PROJECT>] [-c|--configuration] [-f|--framework] [-o|--output] [-r|--runtime] [-v|--verbosity] [--version-suffix]
dotnet publish [-h|--help]
```

---

## <a name="description"></a>Descrizione

`dotnet publish` compila l'applicazione, legge le relative dipendenze specificate nel file di progetto e pubblica il set di file risultante in una directory. L'output conterrà quanto segue:

* Codice linguaggio intermedio (IL) in un assembly con un'estensione *dll*.
* File *.deps.json* contenente tutte le dipendenze del progetto.
* File *.runtime.config.json* che specifica il runtime condiviso previsto dall'applicazione e altre opzioni di configurazione per il runtime, ad esempio il tipo di Garbage Collection.
* Dipendenze dell'applicazione. Questi dati vengono copiati dalla cache NuGet nella cartella di output.

L'output del comando `dotnet publish` è pronto per la distribuzione in un sistema host (ad esempio un server, un computer PC o Mac o un laptop) per l'esecuzione. Questa è l'unica modalità supportata ufficialmente per preparare l'applicazione per la distribuzione. A seconda del tipo di distribuzione specificato dal progetto, nel sistema host il runtime condiviso di .NET Core può essere installato o meno. Per altre informazioni, vedere [Distribuzione di applicazioni .NET Core](../deploying/index.md). Per la struttura di directory di un'applicazione pubblicata, vedere [Directory structure](/aspnet/core/hosting/directory-structure) (Struttura di directory).

## <a name="arguments"></a>Argomenti

`PROJECT`

Progetto da pubblicare che, se non specificato, corrisponde per impostazione predefinita alla directory corrente.

## <a name="options"></a>Opzioni

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

`-c|--configuration {Debug|Release}`

Definisce la configurazione di compilazione. Il valore predefinito è `Debug`.

`-f|--framework <FRAMEWORK>`

Pubblica l'applicazione per il [framework di destinazione](../../standard/frameworks.md) specificato. È necessario specificare il framework di destinazione nel file di progetto.

`--force`

Forza la risoluzione di tutte le dipendenze, anche se l'ultimo ripristino ha avuto esito positivo. Ciò equivale a eliminare il file *project.assets.json*.

`-h|--help`

Stampa una breve guida per il comando.

`--manifest <PATH_TO_MANIFEST_FILE>`

Specifica uno o più [manifesti di destinazione](../deploying/runtime-store.md) da usare per rimuovere il set di pacchetti pubblicati con l'app. Il file manifesto fa parte dell'output del comando [ `dotnet store` ](dotnet-store.md). Per specificare più manifesti, aggiungere un'opzione `--manifest` per ogni manifesto. Questa opzione è disponibile a partire da .NET Core 2.0 SDK.

`--no-dependencies`

Ignora i riferimenti da progetto a progetto e ripristina solo il progetto radice.

`--no-restore`

Non esegue un ripristino implicito quando si esegue il comando.

`-o|--output <OUTPUT_DIRECTORY>`

Specifica il percorso della directory di output. Se non specificato, il percorso predefinito sarà *./bin/[configuration]/[framework]/* per una distribuzione dipendente da framework o *./bin/[configuration]/[framework]/[runtime]* per una distribuzione indipendente.
Se viene specificato un percorso relativo, la directory di output generata è relativa al percorso del file di progetto e non alla directory di lavoro corrente.

`--self-contained`

Pubblica il runtime .NET Core con l'applicazione in modo che non sia necessario installare il runtime nel computer di destinazione. Se viene specificato un identificatore di runtime, il valore predefinito è `true`. Per altre informazioni sui diversi tipi di distribuzione, vedere [Distribuzione di applicazioni .NET Core](../deploying/index.md).

`-r|--runtime <RUNTIME_IDENTIFIER>`

Pubblica l'applicazione per un determinato runtime. Viene usato durante la creazione di una [distribuzione indipendente (SCD, Self-Contained Deployment)](../deploying/index.md#self-contained-deployments-scd). Per un elenco degli identificatori di runtime (RID, Runtime Identifier), vedere il [catalogo RID](../rid-catalog.md). L'impostazione predefinita prevede la pubblicazione di una [distribuzione dipendente da framework (FDD, Framework-Dependent Deployment)](../deploying/index.md#framework-dependent-deployments-fdd).

`-v|--verbosity <LEVEL>`

Imposta il livello di dettaglio del comando. I valori consentiti sono `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]` e `diag[nostic]`.

`--version-suffix <VERSION_SUFFIX>`

Definisce il suffisso di versione che sostituirà l'asterisco (`*`) nel campo del file di progetto relativo alla versione.

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

`-c|--configuration {Debug|Release}`

Definisce la configurazione di compilazione. Il valore predefinito è `Debug`.

`-f|--framework <FRAMEWORK>`

Pubblica l'applicazione per il [framework di destinazione](../../standard/frameworks.md) specificato. È necessario specificare il framework di destinazione nel file di progetto.

`-h|--help`

Stampa una breve guida per il comando.

`--manifest <PATH_TO_MANIFEST_FILE>`

Specifica uno o più [manifesti di destinazione](../deploying/runtime-store.md) da usare per rimuovere il set di pacchetti pubblicati con l'app. Il file manifesto fa parte dell'output del comando [ `dotnet store` ](dotnet-store.md). Per specificare più manifesti, aggiungere un'opzione `--manifest` per ogni manifesto. Questa opzione è disponibile a partire da .NET Core 2.0 SDK.

`-o|--output <OUTPUT_DIRECTORY>`

Specifica il percorso della directory di output. Se non specificato, il percorso predefinito sarà *./bin/[configuration]/[framework]/* per una distribuzione dipendente da framework o *./bin/[configuration]/[framework]/[runtime]* per una distribuzione indipendente.
Se viene specificato un percorso relativo, la directory di output generata è relativa al percorso del file di progetto e non alla directory di lavoro corrente.

`-r|--runtime <RUNTIME_IDENTIFIER>`

Pubblica l'applicazione per un determinato runtime. Viene usato durante la creazione di una [distribuzione indipendente (SCD, Self-Contained Deployment)](../deploying/index.md#self-contained-deployments-scd). Per un elenco degli identificatori di runtime (RID, Runtime Identifier), vedere il [catalogo RID](../rid-catalog.md). L'impostazione predefinita prevede la pubblicazione di una [distribuzione dipendente da framework (FDD, Framework-Dependent Deployment)](../deploying/index.md#framework-dependent-deployments-fdd).

`-v|--verbosity <LEVEL>`

Imposta il livello di dettaglio del comando. I valori consentiti sono `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]` e `diag[nostic]`.

`--version-suffix <VERSION_SUFFIX>`

Definisce il suffisso di versione che sostituirà l'asterisco (`*`) nel campo del file di progetto relativo alla versione.

---

## <a name="examples"></a>Esempi

Pubblicare il progetto nella directory corrente:

`dotnet publish`

Pubblicare l'applicazione usando il file di progetto specificato:

`dotnet publish ~/projects/app1/app1.csproj`
    
Pubblicare il progetto nella directory corrente usando il framework `netcoreapp1.1`:

`dotnet publish --framework netcoreapp1.1`
    
Pubblicare l'applicazione corrente usando il framework `netcoreapp1.1` e il runtime per `OS X 10.10`. Questo identificatore di runtime deve essere elencato nel file di progetto.

`dotnet publish --framework netcoreapp1.1 --runtime osx.10.11-x64`

## <a name="see-also"></a>Vedere anche

* [Framework di destinazione](../../standard/frameworks.md)
* [Catalogo RID (Runtime IDentifier)](../rid-catalog.md)
