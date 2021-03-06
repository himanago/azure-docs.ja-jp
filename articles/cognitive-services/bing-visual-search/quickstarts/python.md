---
title: 'クイック スタート: 視覚検索クエリを作成する (Python) - Bing Visual Search'
titleSuffix: Azure Cognitive Services
description: Bing Visual Search API にイメージをアップロードし、そのイメージに関する分析情報を取得する方法を示します。
services: cognitive-services
author: swhite-msft
manager: cgronlun
ms.service: cognitive-services
ms.component: bing-visual-search
ms.topic: quickstart
ms.date: 5/16/2018
ms.author: scottwhi
ms.openlocfilehash: 3a0d92e42eed097e244118a60ec0a4223c9cedf5
ms.sourcegitcommit: 5aed7f6c948abcce87884d62f3ba098245245196
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2018
ms.locfileid: "52440943"
---
# <a name="quickstart-your-first-bing-visual-search-query-in-python"></a>クイック スタート: Python での最初の Bing Visual Search クエリ

Bing Visual Search API は、提供された画像に関する情報を返します。 イメージを提供するには、イメージの URL または分析情報トークンを使用するか、イメージをアップロードします。 これらのオプションの詳細については、「[Bing Visual Search API とは](../overview.md)」を参照してください。 この記事では、イメージのアップロードについて説明します。 よく知られているランドマークの写真を撮影し、それに関する情報を取得するモバイル シナリオで、イメージのアップロードは便利であると考えられます。 たとえば、分析情報にはランドマークに関する雑学が含まれることがあります。 

ローカル イメージをアップロードする場合は、次に示すフォーム データを POST の本文に含める必要があります。 フォーム データには Content-Disposition ヘッダーが含まれる必要があります。 その `name` パラメーターには "image" を設定する必要があり、`filename` パラメーターには任意の文字列を設定できます。 フォームの内容は、イメージのバイナリです。 アップロードできるイメージの最大サイズは、1 MB です。 

```
--boundary_1234-abcd
Content-Disposition: form-data; name="image"; filename="myimagefile.jpg"

ÿØÿà JFIF ÖÆ68g-¤CWŸþ29ÌÄøÖ‘º«™æ±èuZiÀ)"óÓß°Î= ØJ9á+*G¦...

--boundary_1234-abcd--
```

この記事では、Bing Visual Search API 要求を送信し、JSON 検索結果を表示するシンプルなコンソール アプリケーションを紹介します。 このアプリケーションは Python で記述されていますが、API は、HTTP 要求の発行と JSON の解析が可能な任意のプログラミング言語と互換性がある RESTful Web サービスです。 

## <a name="prerequisites"></a>前提条件

このコードを実行するには、[Python 3](https://www.python.org/) が必要です。

このクイック スタートでは、「[Cognitive Services の価格 - Bing Search API](https://azure.microsoft.com/en-us/pricing/details/cognitive-services/search-api/)」に記載されている S9 価格帯のサブスクリプションを開始する必要があります。 

Azure portal でサブスクリプションを開始するには、次の手順に従います。
1. Azure portal の一番上の "`Search resources, services, and docs`" と表示されているテキスト ボックスに「BingSearchV7」と入力します。  
2. ドロップダウン リストの [Marketplace] から `Bing Search v7` を選択します。
3. 新しいリソースの名前を [`Name`] に入力します。
4. `Pay-As-You-Go` サブスクリプションを選択します。
5. `S9` 価格レベルを選択します。
6. [`Enable`] をクリックしてサブスクリプションを開始します。

## <a name="running-the-walkthrough"></a>チュートリアルの実行

このアプリケーションを実行するには、次の手順に従います。

1. 普段ご利用の IDE またはエディターで新しい Python プロジェクトを作成します。
2. visualsearch.py という名前のファイルを作成し、このクイック スタートにあるコードを追加します。
3. `SUBSCRIPTION_KEY` 値を、サブスクリプション キーに置き換えます。
3. `imagePath` 値を、アップロードするイメージのパスに置き換えます。
4. プログラムを実行します。



次のコードは、Python 内のマルチパート フォーム データを使用してメッセージを送信する方法を示しています。

```python
"""Bing Visual Search upload image example"""

# Download and install Python at https://www.python.org/
# Run the following in a command console window
# pip3 install requests

import requests, json


BASE_URI = 'https://api.cognitive.microsoft.com/bing/v7.0/images/visualsearch'

SUBSCRIPTION_KEY = '<yoursubscriptionkeygoeshere>'

HEADERS = {'Ocp-Apim-Subscription-Key': SUBSCRIPTION_KEY}

imagePath = '<pathtoyourimagetouploadgoeshere>'

file = {'image' : ('myfile', open(imagePath, 'rb'))}

def main():
    
    try:
        response = requests.post(BASE_URI, headers=HEADERS, files=file)
        response.raise_for_status()
        print_json(response.json())

    except Exception as ex:
        raise ex


def print_json(obj):
    """Print the object as json"""
    print(json.dumps(obj, sort_keys=True, indent=2, separators=(',', ': ')))



# Main execution
if __name__ == '__main__':
    main()
```


## <a name="next-steps"></a>次の手順

[分析情報トークンを使用してイメージに関する分析情報を取得する](../use-insights-token.md)  
[Bing Visual Search 画像アップロードのチュートリアル](../tutorial-visual-search-image-upload.md)
[Bing Visual Search シングルページ アプリのチュートリアル](../tutorial-bing-visual-search-single-page-app.md)  
[Bing Visual Search の概要](../overview.md)  
[試してみる](https://aka.ms/bingvisualsearchtryforfree)  
[無料試用版のアクセス キーを入手する](https://azure.microsoft.com/try/cognitive-services/?api=bing-visual-search-api)  
[Bing Visual Search API のリファレンス](https://aka.ms/bingvisualsearchreferencedoc)
