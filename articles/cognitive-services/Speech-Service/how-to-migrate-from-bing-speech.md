---
title: Bing Speech から Speech Service に移行する
titleSuffix: Azure Cognitive Services
description: 開発者の観点から Bing Speech と Speech Service の違いを確認し、Speech Service を使用するようにアプリケーションを移行します。
services: cognitive-services
author: wsturman
manager: cgronlun
ms.service: cognitive-services
ms.component: speech-service
ms.topic: conceptual
ms.date: 10/01/2018
ms.author: gracez
ms.openlocfilehash: fdd22e14e0b7636dbc337a20dd69bf93696bb924
ms.sourcegitcommit: 6135cd9a0dae9755c5ec33b8201ba3e0d5f7b5a1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/31/2018
ms.locfileid: "50416282"
---
# <a name="migrate-from-bing-speech-to-the-speech-service"></a>Bing Speech から Speech Service に移行する

アプリケーションを Bing Speech API から Speech Service に移行するにあたっては､この記事を参考にしてください｡

この記事では、Bing Speech API と Speech Service の違いを簡単に説明し、アプリケーションの移行方法を提案します。 Speech Service によって Bing Speech API サブスクリプション キーが受け付けられることはありません｡新たに Speech Service サブスクリプションが必要です｡

1 つの Speech Service サブスクリプション キーで、次の機能にアクセスできます。 それぞれが個別に測定されるため、課金は使用した機能に対するものだけです。

* [音声テキスト変換](speech-to-text.md)
* [カスタム音声テキスト変換](https://cris.ai)
* [テキスト読み上げ](text-to-speech.md)
* [カスタム テキスト音声読み上げ](how-to-customize-voice-font.md)
* [音声翻訳](speech-translation.md) ([テキスト翻訳](../translator/translator-info-overview.md)は含まれません)

[Speech SDK](speech-sdk.md) は Bing Speech クライアント ライブラリの機能を代替するものですが､使用している API は異なります｡

## <a name="comparison-of-features"></a>機能の比較

Speech Service と Bing Speech はよく似ていますが、次のような違いがあります。

機能 | Bing Speech | Speech Service | 詳細
-|-|-|-
C++ SDK | :heavy_minus_sign: | :heavy_check_mark: | Speech Service は Windows および Linux に対応します。
Java SDK | :heavy_check_mark: | :heavy_check_mark: | Speech Service は Android および Speech Devices に対応します。
C# SDK | :heavy_check_mark: | :heavy_check_mark: | Speech Service は、Windows 10、Universal Windows Platform (UWP)、および .NET Standard 2.0 に対応します。
連続音声認識 | 10 分 | 無制限 (SDK) | Bing Speech と Speech Service WebSockets プロトコルは､どちらも呼び出し 1 回あたり最大 10 分をサポートしています｡ ただし､Speech SDK 方はタイムアウト時に自動的に再接続､切断します｡
部分的または中間結果 | :heavy_check_mark: | :heavy_check_mark: | WebSockets プロトコルまたは SDK あり。
カスタム音声モデル | :heavy_check_mark: | :heavy_check_mark: | Bing Speech には別個の Custom Speech サブスクリプションが必要です。
カスタム音声フォント | :heavy_check_mark: | :heavy_check_mark: | Bing Speech には別個の Custom Voice サブスクリプションが必要です。
24KHz の音声 | :heavy_minus_sign: | :heavy_check_mark: 
音声意図認識 | 別途 LUIS API 呼び出しが必要 | 統合済み (SDK) |  Speech Service では LUIS キーを利用できます。
簡単な意図認識 | :heavy_minus_sign: | :heavy_check_mark: 
長い音声ファイルの一括文字起こし | :heavy_minus_sign: | :heavy_check_mark:
認識モード | エンドポイント URI 経由での手動 | 自動 | Speech Service には認識モードはありません。
エンドポイントの地域性 | グローバル | 地域 | 地域のエンドポイントによって､待機時間が改善されます｡
REST API | :heavy_check_mark: | :heavy_check_mark: | Speech Service REST API は Bing Speech と互換性があります (エンドポイントは異なる)｡ REST API はテキスト読み上げ機能と音声テキスト変換機能(限定的) をサポートしています｡
WebSockets プロトコル | :heavy_check_mark: | :heavy_check_mark: | Speech Service WebSockets API は Bing Speech と互換性があります (エンドポイントは異なる)｡ 可能であれば、Speech SDK に移行することで、コードを簡略化できます。
Service-to-service API 呼び出し | :heavy_check_mark: | :heavy_minus_sign: | Bing Speech では､C# サービス ライブラリで提供｡ 
オープン ソース SDK | :heavy_check_mark: | :heavy_minus_sign: |

Speech Service では､トランザクション ベースではなく時間ベースの価格モデルが採用されています｡ 詳しくは、[Speech Service の価格](https://azure.microsoft.com/pricing/details/cognitive-services/speech-services/)に関するページをご覧ください。

## <a name="migration-strategies"></a>移行方法

Bing Speech API を使用しているアプリケーションを開発中の場合､あるいはそうしたアプリケーションを運用している場合は､できるかぎり速やかに Speech Service を使用するように更新することをお勧めします｡ 使用できる SDK やサンプル コード､チュートリアルについては､[Speech Service のドキュメント](index.yml)をご覧ください｡

Speech Service の [REST API](rest-apis.md) Bing Speech の API 互換性があります｡ 現在 Bing Speech REST API をご利用の場合は、REST エンドポイントのみを変更し、Speech Service サブスクリプション キーに切り替えるだけで済みます。

Speech Service WebSockets プロトコルも Bing Speech が使用しているものと互換性があります｡ 新しい開発では、WebSocket ではなく Speech Service SDK を使用することをお勧めします。 既存のコードもこの SDK に移行することをお勧めします。 REST API 同様､既存のコードが WebSockets を介して Bing Speech を使用している場合は､エンドポイントを変更して､キーを更新すればよいだけです｡

ただし、特定のプログラミング言語で Bing Speech クライアント ライブラリを使用している場合、[Speech SDK](speech-sdk.md) に移行するには、API が異なるため、アプリケーションそのものを変更する必要があります。 Speech SDK により、新しい機能を利用できる一方でコードを簡略化できるようになります。

現在､Speech SDK は C# (Windows 10､UWP､.NET Standard) と Java (Android とカスタム デバイス)､, Objective C (iOS)､C++ (Windows と Linux)､および JavaScript に対応しています｡ どのプラットフォームの API も似ており､マルチプラットフォーム開発が容易になります｡

現在､Speech Service はグローバル エンドポイントを提供していません｡ アプリケーションのすべてのトラフィックに単一のリージョン エンドポイントを使用しているときにアプリケーションが効率的に機能するかどうかを判断します。 効率的に機能しない場合は､geolocation を使って最も効率的なエンドポイントを探してください｡ 使用するリージョンごとに Speech Service サブスクリプションが必要になります。

アプリケーションが長時間維持される接続を使用していて、利用可能な SDK を使用できない場合は、WebSocket 接続を使用できます。 適切なタイミングで再接続して、10 分のタイムアウト制限を管理してください。

Speech SDK を使ってみる

1. [Speech SDK](speech-sdk.md) をダウンロードします｡
1. Speech Service [クイック スタート ガイド](quickstart-csharp-dotnet-windows.md)と[チュートリアル](how-to-recognize-intents-from-speech-csharp.md)に従って作業します。 また、[コード サンプル](samples.md)を見て、新しい API に関する経験を得ます。
1. Speech Service とその API を使用するようにアプリケーションを更新します。

## <a name="support"></a>サポート

Bing Speech のお客様は[サポート チケット](https://ms.portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/newsupportrequest)を開いて､カスタマー サービスに問い合わせることをお勧めします｡ サポートで[テクニカル サポート プラン](https://azure.microsoft.com/support/plans/)が必要な場合もお問い合わせください。

Speech Service､SDK､および API サポートについては､Speech Service の[サポート ページ](support.md)をご覧ください｡

## <a name="next-steps"></a>次の手順

* [Speech Service を無料で試す](get-started.md)
* [クイック スタート: UWP アプリで Speech SDK を使用して音声を認識する](quickstart-csharp-uwp.md)

## <a name="see-also"></a>関連項目
* [Speech Service リリース ノート](releasenotes.md)
* [Speech Service とは](overview.md)
* [Speech Service および Speech SDK のドキュメント](speech-sdk.md#get-the-sdk)
