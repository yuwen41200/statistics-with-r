Week 16 Practice 1
================
Yu-Wen Pu
2018-06-12

crawl webpages
--------------

``` r
knitr::opts_chunk$set(results = "hold", fig.retina = 2)
set.seed(1830)
```

### 網頁標題

``` r
library(rvest)
```

    ## Loading required package: xml2

``` r
url <- "https://www.ptt.cc/bbs/movie/M.1525705635.A.9D1.html"
(content <- read_html(url))
```

    ## {xml_document}
    ## <html>
    ## [1] <head>\n<meta http-equiv="Content-Type" content="text/html; charset= ...
    ## [2] <body>\n\t\t\n<div id="fb-root"></div>\n<script>(function(d, s, id)  ...

``` r
(title_node <- html_nodes(content, xpath = "//title"))
```

    ## {xml_nodeset (1)}
    ## [1] <title>[好雷] 復仇者聯盟3－夕陽下瑟縮的無力英雄 - 看板 movie - 批踢踢實業坊</title>\n

``` r
(title <- html_text(title_node))
```

    ## [1] "[好雷] 復仇者聯盟3－夕陽下瑟縮的無力英雄 - 看板 movie - 批踢踢實業坊"

### 作者、標題、時間

``` r
(ns <- html_nodes(content, xpath = "//div[@class='article-metaline']"))
```

    ## {xml_nodeset (3)}
    ## [1] <div class="article-metaline">\n<span class="article-meta-tag">作者</s ...
    ## [2] <div class="article-metaline">\n<span class="article-meta-tag">標題</s ...
    ## [3] <div class="article-metaline">\n<span class="article-meta-tag">時間</s ...

``` r
(n <- html_nodes(ns[1], xpath = "span[@class='article-meta-value']"))
```

    ## {xml_nodeset (1)}
    ## [1] <span class="article-meta-value">twoquarters (半個比爾)</span>

``` r
(t <- html_text(n))
```

    ## [1] "twoquarters (半個比爾)"

``` r
html_text(html_nodes(ns[2], xpath = "span[@class='article-meta-value']"))
```

    ## [1] "[好雷] 復仇者聯盟3－夕陽下瑟縮的無力英雄"

``` r
html_text(html_nodes(ns[3], xpath = "span[@class='article-meta-value']"))
```

    ## [1] "Mon May  7 23:07:08 2018"

### 內文

``` r
post <- html_text(html_nodes(content, xpath = "//div[@id='main-content']/text()"))
head(post, n = 3)
```

    ## [1] "\n網誌圖文好讀版："                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             
    ## [2] "\n\n十年前，《鋼鐵人》的上映，象徵漫威宇宙的開始，當時，沒有太多人知道鋼鐵人是誰，\n\n東尼史塔克是誰。十年後，《復仇者聯盟：無限之戰》的上映，卻讓許多影迷趨之若鶩，\n\n這部漫威花費十年鋪陳的作品，卻在最後讓人倒抽一口氣，靜靜蜷縮在座位上。過去看似\n\n威猛的英雄們，遇上薩諾斯的強大卻是如此無力，面對全然公平的機率卻顯得無比脆弱。\n\n以前只要復仇者團結一心，沒有過不了的難關。如今，再多努力卻未必能得到好的結果，\n\n甚至讓人更加絕望。最令人不捨的，正是英雄拚盡全力試圖阻止災難發生，卻被命運無情\n\n擺佈，徒留滿滿悔恨與遺憾。\n\n\n---------------貼----心----防----雷----線-----------------\n\n\n\n\n\n\n\n\n\n\n\n"                                                                                                                                                                                                                                                                                                                                                                                                                                             
    ## [3] "\n\n\n以往，漫威劇情走的多半是歡樂與正面的路線，其中，洛基的「假死」更是許多粉絲相當\n\n熟悉的。擅長用幻術愚弄眾人的他，死亡的表象更是他的拿手絕活。因此，如果要使影迷\n\n相信這是嚴肅的作品，真正的賜死洛基，將有極大的宣示作用。\n\n\n然而，薩諾斯的強大，不只是他輕易奪走洛基性命，而且他單憑格鬥技巧就撂倒浩克。還\n\n記得《復仇者聯盟》中，浩克把洛基痛扁一頓，還烙下狠話：「好弱的神！」可是，當他\n\n正面遭遇薩諾斯，甚至讓洛基興奮的說出「我們有浩克」，結果卻被打趴在地。於此，薩\n\n諾斯的強度表露無遺，不但比阿斯嘉神族還要強大，更比浩克來的威猛。\n\n\n對於索爾來說，他已經失去太多了，父親的死，阿斯嘉的毀滅，好不容易帶著人民逃出生\n\n天，卻遇上意圖奪取宇宙魔方的薩諾斯。更悲慘的是，他目睹了洛基的死去，不管洛基多\n\n麼喜歡惡作劇，背叛自己多少次，但他終究是那唯一的弟弟，是陪他度過無數考驗與苦難\n\n的手足。\n\n\n當洛基喉嚨被捏碎的聲音傳出，索爾卻只能無力的被束縛著，發出模糊的「No!」來表達\n\n悲痛。過去老是出賣自己的弟弟，奮力挺身而出，還向自己承諾兩人還能一同見到明天的\n\n太陽，沒想到卻又是無法實現的謊言。但這個謊言，卻令人心碎不已。\n\n\n"

``` r
post <- paste(post, collapse = "。")
substr(post, 1, 500)
```

    ## [1] "\n網誌圖文好讀版：。\n\n十年前，《鋼鐵人》的上映，象徵漫威宇宙的開始，當時，沒有太多人知道鋼鐵人是誰，\n\n東尼史塔克是誰。十年後，《復仇者聯盟：無限之戰》的上映，卻讓許多影迷趨之若鶩，\n\n這部漫威花費十年鋪陳的作品，卻在最後讓人倒抽一口氣，靜靜蜷縮在座位上。過去看似\n\n威猛的英雄們，遇上薩諾斯的強大卻是如此無力，面對全然公平的機率卻顯得無比脆弱。\n\n以前只要復仇者團結一心，沒有過不了的難關。如今，再多努力卻未必能得到好的結果，\n\n甚至讓人更加絕望。最令人不捨的，正是英雄拚盡全力試圖阻止災難發生，卻被命運無情\n\n擺佈，徒留滿滿悔恨與遺憾。\n\n\n---------------貼----心----防----雷----線-----------------\n\n\n\n\n\n\n\n\n\n\n\n。\n\n\n以往，漫威劇情走的多半是歡樂與正面的路線，其中，洛基的「假死」更是許多粉絲相當\n\n熟悉的。擅長用幻術愚弄眾人的他，死亡的表象更是他的拿手絕活。因此，如果要使影迷\n\n相信這是嚴肅的作品，真正的賜死洛基，將有極大的宣示作用。\n\n\n然而，薩諾斯的強大，不只是他輕易奪走洛基性命，而且他單憑格鬥技巧就撂倒浩克。還\n\n記得《"

### 備註：語法說明

``` r
x <- 2
y <- c("a", "b", "c", "d")
paste(1, x, sep = "+")
paste(y, collapse = "_")
paste(1, y, sep = "+", collapse = "_")
```

    ## [1] "1+2"
    ## [1] "a_b_c_d"
    ## [1] "1+a_1+b_1+c_1+d"

### 斷詞

``` r
library(jiebaR)
```

    ## Warning: package 'jiebaR' was built under R version 3.4.4

    ## Loading required package: jiebaRD

``` r
cut <- worker()
new_user_word(cut, "薩諾斯", "n")
words <- cut[post]
words <- words[nchar(words) > 1]
head(words)
```

    ## [1] TRUE
    ## [1] "網誌" "圖文" "讀版" "十年" "鋼鐵" "上映"

``` r
results <- data.frame(table(words))
results <- results[order(results$Freq, decreasing = TRUE), ]
head(results)
```

    ##      words Freq
    ## 331 薩諾斯   21
    ## 569   自己   13
    ## 86    東尼    8
    ## 240   洛基    8
    ## 524   宇宙    7
    ## 413   完成    5

### 文字雲

``` r
library(wordcloud2)
results <- results[results$Freq > 1, ]
wordcloud2(results)
```

<!--html_preserve-->

<script type="application/json" data-for="htmlwidget-1d6711dcd48e238db9a2">{"x":{"word":["薩諾斯","自己","東尼","洛基","宇宙","完成","無法","最後","復仇者","靈魂","令人","人類","甚至","生命","泰坦","無比","無力","真的","只能","寶石","不已","才能","地球","發生","感覺","鋼鐵","更加","過去","換取","結果","馬爾薩斯","漫威","沒有","目睹","強大","然而","認為","如此","生靈","十年","塔克","唯有","我們","相信","許多","眼前","遺憾","英雄","拯救","最終","QQ","阿斯","半數","比起","成為","成員","代價","當他","得到","弟弟","電影","東尼史","動手","多少","奪取","粉絲","父親","付出","感到","葛摩","更是","公平","觀眾","浩克","謊言","機率","記得","家人","絕望","渴望","肯定","恐慌","盔甲","來說","聯盟","落敗","面對","面前","抹消","母親","內心","努力","其實","強度","卻是","如果","如今","瑟縮","上映","勝利","失去","實現","始終","試圖","死去","死亡","索爾","天空","完美","威猛","未來","無情","無數","無限","犧牲","喜愛","喜歡","相當","想法","心愛","心碎","星上","興奮","一半","一口氣","因為","影迷","有趣","遇上","戰鬥","這樣","正面","只是","資源","作品","Valentine"],"freq":[21,13,8,8,7,5,5,5,4,4,4,4,4,4,4,4,4,4,4,3,3,3,3,3,3,3,3,3,3,3,3,3,3,3,3,3,3,3,3,3,3,3,3,3,3,3,3,3,3,3,3,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2],"fontFamily":"Segoe UI","fontWeight":"bold","color":"random-dark","minSize":0,"weightFactor":8.57142857142857,"backgroundColor":"white","gridSize":0,"minRotation":-0.785398163397448,"maxRotation":0.785398163397448,"shuffle":true,"rotateRatio":0.4,"shape":"circle","ellipticity":0.65,"figBase64":null,"hover":null},"evals":[],"jsHooks":{"render":[{"code":"function(el,x){\n                        console.log(123);\n                        if(!iii){\n                          window.location.reload();\n                          iii = False;\n\n                        }\n  }","data":null}]}}</script>
<!--/html_preserve-->
