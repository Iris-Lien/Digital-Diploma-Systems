# 以區塊鏈及去中心化儲存IPFS建置的校園畢業證書發放系統

<img src="https://user-images.githubusercontent.com/56546170/136023481-a91fd318-f5c7-4ed4-9a43-c095320c6dd3.png" width="400">  

## 摘要
畢業證書是專業能力及教育程度的證明，證書的發放是經由校方審查通過後給予。在升學、求職的審查過程中，我們常需要提交畢業證書。一般而言，畢業證書的發放及遺失補發的程序較為繁瑣。企業及教育單位、人力銀行為了審查證書的正確完整性，需要時間、人力的消耗。本專題提出以區塊鏈及去中心化儲存技術建置校園畢業證書發放系統。本專題使用以太坊中的智能合約將畢業證書的資訊紀錄於以太坊中。為了更安全、可靠地使用去中心化儲存系統，我們將畢業證書佈置於星際檔案系統IPFS。 IPFS 是已經有完整的API的成熟系統，在撰寫Script APP時容易，且作為儲存系統的可靠性高。

## 前言
畢業證書不僅代表著完成的學業及所學，也證明自己的能力。在升學、求職的書面審查過程，常需要提交畢業證書。
因此，我們有需要確保畢業證書的正確、完整性，以防止偽造證書、學歷，而通過審查。
另外，企業及教育單位、人力銀行 (註: 近年透過人力銀行招聘網站求職與找人才愈來愈多)，為了審查證書的正確性，則需更繁瑣謹慎的流程。
這些導致了時間成本過高、及人力資源消耗。偽造假學位、非法學位不僅是誠信問題。若是太猖獗絕也會導致研究和高等學校教育系統的崩潰，這在很多發展中國家都有先例。
本專題目的是藉由區塊鏈及去中心化儲存技術，完成畢業證書發放系統並解決上述問題。讓發放證書、驗證更便捷與正確。區塊鏈是一種分散式的驗證技術，使用區塊鏈可確保資料的完整性與安全性。
但是以太坊區塊鏈，每個區塊都有gas限制，其所能容納的交易有限，不能存儲大容量文件。所以我們擬以去中心化儲存系統，來存儲畢業證書。

國家高速網路與計算中心區塊鏈團隊，配合台中市政府智慧校園之推廣，已經開發了畢業證書區塊鏈驗證系統平台。提供臺中市政府中、小學試用畢業證書的驗證。
他們是使用去中心化星際檔案系統 (IPFS)。因IPFS 有完整的API，在撰寫Script APP時相對容易，故是極佳的選擇。
由於畢業證書的發放及驗證，需有極高的可靠度，本專題的校園畢業證書發放系統使用去中心儲存系統IPFS，IPFS是完全開源的，可以和以太坊區塊鏈配合，達到事半功倍及可靠度。

## 動機
傳統上，第三方機構要驗證學生的畢業證書真偽，需要向學校教務處提出查詢，教務處職員在予以回覆。 學生在申請補發證書時，亦需向教務處提出申請，審核後再製作寄送，過程較為繁瑣、冗長。
因此，我們擬定植基於區塊鏈去中心化儲存系統，完成校園畢業證書發放。

我們使用去中心儲存系統IPFS，也就是星際檔案系統，它類似於在一個Gitrepositor的BitTorrent群彼此交換資料，每個節點皆為使用BitTorrent Protocol上交換資料，
而資料的版本控制則是經由Merkle DAG去完成，並提供高通量處理的塊存儲模型，可以將數據分片儲存在分散式的節點。下載時可從多個節點中獲取，降低儲存的成本，提升數據下載速度。
資料分散到不同的節點，因此難以成為攻擊對象。另外，IPFS 有完整的API，在撰寫Script APP時相對容易，這是我們選擇它來當主要系統的原因。

## 系統設計概念
本專題所提及的畢業證書發放、查證系統是利用智能合約將證書的有效性寫上區塊鏈中以達到不可竄改、可靠的查證系統。區塊鏈及去中心化儲存的校園畢業證書發放系統架構圖如下
<img src="https://github.com/Iris-Lien/Digital-Diploma-Systems/blob/main/%E6%9E%B6%E6%A7%8B%E5%9C%96.jpg" width="800">

區塊鏈及去中心化儲存的校園畢業證書發放系統包含了發證單位(學校)、憑證擁有者(學生)、和驗證單位(企業、教育機構、人力銀行)。
這三個實體，我們分別以發證學校單位(S)、憑證擁有者學生(O)、和憑證驗證單位(V)來表示。下面顯示了本系統的三個部分，包括畢業證書上傳階段、畢業證書下載階段、和第三方畢業證書驗證階段。
本專題的登入及註冊網站都是架設於Prepros前端軟體，除了產生可以跨裝置的網址外，還可以編譯相當多語言，且內建http伺服器，拿來做web開發是很合適的，詳細說明如下

**【階段1】校方上傳畢業證書及資訊階段**

    這個階段包含了校方對學生的畢業證書上傳與撤銷。

    (步驟 1-1) S審核完O的畢業資格後，將O資料與電子畢業證書儲存於學校主伺服器網站。
    
    (註: 學校保留完整、詳細資料，以利日後查核)。

    (步驟 1-2) 學校主伺服器網站將學生畢業證書、及相關資料上傳至IPFS去中心化儲存系統。

    (步驟  1-3) IPFS回傳S其雜湊位址，並記錄於學校主伺服器網站。

    (步驟  1-4、1-5) S將畢業證書有效性查核資料，寫入智能合約，上傳至以太坊區塊鏈。

    註: 若S需要撤銷O的畢業證書，即可透過更改有效性變數來達成。

**【階段2】學生下載畢業證書階段**

    這個階段包含了學生下載取得畢業證書。

    (步驟 2-1) O至S網站登入驗證其身分正確性。若正確則可登入頁面並獲得證書連結。

    (步驟 2-2) 驗證成功，將O的證書雜湊位址回傳給O，讓其獲得證書連結並下載證書。
    
**【階段3】第三方畢業證書驗證階段**

    此階段包含了第三方(企業、教育機構、人力銀行等)，對學生畢業證書的驗證。
    
    驗證過程，我們採用在畢業證書上附加QR碼的方式，證書紙本樣本及證書資訊頁面如下
    
    (步驟 3-1) V由O所提的畢業證書紙本樣張(如圖5)，或電子証書，取得QR碼。
    
    (步驟 3-2、3-3) V透過QR碼掃描，透過智能合約連至以太坊區塊鏈做O的畢業證書有效性驗証。
    
    由於區塊鏈的不可竄改性，我們可以保證資料的可信度。
    
此時QR碼用於證書有效性之驗證，透過QR碼連線API，使用智能合約裡的內容驗證學生畢業證書相關資料的正確性，以及確認該學生的畢業證書確實是有上傳至IPFS。
前面提到的證書撤銷作業，所以若是S透過智能合約將O的畢業證書撤銷、廢除，則V可在數位畢業證書資訊中看到相關的有效性欄位變更為"Invalid"無效，
且該頁面下方的QR碼可連接至該位學生於IPFS上的畢業證書，證實為有此學生之畢業證書。

<img src="https://github.com/Iris-Lien/Digital-Diploma-Systems/blob/main/%E5%9C%96%E7%89%872.png" width="800">
    
## 開發環境及軟體
### Remix IDE
Solidity是一種合約導向語言，可用於部屬合約於各種不同的區塊鏈平台上。
透過線上編譯器Remix IDE 作為編譯的環境，完成編譯，將程式碼編譯成二進制(Contract Bytecode)後，才部屬於EVM。
* 線上版連結 http://remix.ethereum.org

### MetaMask
ETH 錢包 MetaMask，它是一個 Chrome 插件錢包，可以讓使用者跟以太坊的智能合約互動。
* 下載連結 https://metamask.io/

### IPFS
去中心化儲存系統不需要中央服務器，而是將數據資料存儲和分發到網絡的不同節點。
將儲存資源組合統一，然後通過簡單友好的管理介面或API提供給用戶簡單、個性化的儲存解決方案。
* 下載連結 https://ipfs.io/
* 切換至ipfs下載後的檔案目錄
``` 
cd ./Go-ipfs
```
* 啟動節點
``` 
ipfs daemon
```
* 選擇要上傳的檔案路徑 
``` 
add ./data.jpg
```

### Prepros
* 下載連結 https://prepros.io/
* 點選左下方Add Project導入專案

<img src="https://user-images.githubusercontent.com/56546170/119266865-0b07ca00-bc1f-11eb-8dac-861b7902e6e1.png" width="800">

* 右鍵選取要打開的檔案即可開啟網頁(其他人也可透過這個網址連結)

<img src="https://user-images.githubusercontent.com/56546170/119266914-3be7ff00-bc1f-11eb-89f9-98a965bfbfc4.png" width="800">

## 成果展示
* 點此連結觀看展示影片 https://www.youtube.com/watch?v=cib09eeP7yY

## 結論
本專題植基於區塊鏈及去中心化儲存系統IPFS來建置校園畢業證書發放系統，除了IPFS外Swarm也是個不錯的選擇，Swarm由以太坊基金會所成立並且是自身發展的去中心化檔案系統。
它是以太坊為Web3提供各種基礎層服務，包括節點到節點消息傳遞，媒體流，分散式數據庫服務以及可分散式服務。
未來期許將IPFS當作主要系統，並且用Swarm來作為備份系統，可以使這兩者與以太坊區塊鏈配合，達到事半功倍與穩定。

現階段本專題遇到的困難為因智能合約發佈在測試鏈上，網站須依靠MetaMask錢包才能和智能合約進行連結，再者為QR碼經由錢包掃描後會對網域進行加密，造成網址錯誤無法正常導向，因此需手動更改網域才可前往正確網站查看證書資訊，未來上若有完善的伺服器提供架設網站或許可解決此問題。

本專題利用區塊鏈去中心化之特性，簡化校方發證、學生補發、第三方驗證的作業花費時間。數位電子畢業證書，不僅改善畢業證書發放工作及流程，可有效防止偽造情況。透過區塊鏈可大幅降低驗證程序的時間及人力資源消耗，對於證書真實性更加有保障，除非攻擊者發起51%攻擊。
