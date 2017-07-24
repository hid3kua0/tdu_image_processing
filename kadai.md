# 画像処理工学　課題
  
<gahag-0016161186-1.jpg> を原画像とする。この画像は、縦598×横900のディジタルカラー画像である。  
  
課題1  
画像をダウンサンプリングして(標本化間隔を大きくして)表示せよ。  
  
    ORG=imread('gahag-0016161186-1.jpg'); % 原画像の入力  
    imagesc(ORG); axis image; % 画像の表示  
  
によって原画像を読み込み、表示した画像を図1に示す。  
  
![ex1_1](https://github.com/hid3kua0/tdu_image_processing/blob/master/kadaipic/ex1_1.png)  
  
図1　原画像  
  
原画像を1/2サンプリングするには、画像を1/2倍に縮小した後、2倍に拡大すればよい。なお、拡大する際は単純補間するために「box」オプションを設定する。  
  
    IMG = imresize(IMG,0.5); % 画像の縮小  
    IMG2 = imresize(IMG,4,'box'); % 画像の拡大  
  
1/2サンプリングの結果を図2に示す。  
  
![ex1_2](https://github.com/hid3kua0/tdu_image_processing/blob/master/kadaipic/ex1_2.png)  
   
図2　1/2サンプリング画像  
  
同様に原画像を1/4サンプリングするには、1/2サンプリング画像をさらに1/2倍に縮小した後、2倍に拡大すればよい。  
即ち、  
  
    IMG = imresize(IMG,0.5); % 画像の縮小  
    IMG2 = imresize(IMG,4,'box'); % 画像の拡大  
  
とする。1/4サンプリングの結果を図3に示す。  
  
![ex1_3](https://github.com/hid3kua0/tdu_image_processing/blob/master/kadaipic/ex1_3.png)  
  
図3　1/4サンプリング画像  
  
1/8から1/32サンプリングも同様に  
  
    IMG = imresize(IMG,0.5); % 画像の縮小  
    IMG2 = imresize(IMG,4,'box'); % 画像の拡大  
  
の処理を繰り返す。各サンプリングの結果を図4～6に示す。  
  
![ex1_4](https://github.com/hid3kua0/tdu_image_processing/blob/master/kadaipic/ex1_4.png)  
  
図4　1/8サンプリング画像  
  
![ex1_5](https://github.com/hid3kua0/tdu_image_processing/blob/master/kadaipic/ex1_5.png)  
  
図5　1/16サンプリング画像  
  
![ex1_6](https://github.com/hid3kua0/tdu_image_processing/blob/master/kadaipic/ex1_6.png)  
  
図6　1/32サンプリング画像  
  
このように、サンプリング幅を大きくするほど、モザイク状のサンプリング歪みが顕著になっていく。  
   
   
課題2  
2階調、4階調、8階調の画像を生成せよ。  
  
    ORG=imread('gahag-0016161186-1.jpg'); % 原画像の入力  
    ORG = rgb2gray(ORG); colormap(gray); colorbar;  
  
により、原画像を白黒濃淡画像化する。なお、以降の課題においてもこの白黒濃淡画像を使用する。   
白黒濃淡画像化された原画像を図7に示す。  
  
![ex2_1](https://github.com/hid3kua0/tdu_image_processing/blob/master/kadaipic/ex2_1.png)  
  
図7　白黒濃淡画像化された原画像  
  
原画像を2階調にするには、原画像の輝度値が256階調なので、128を閾値としてこれより大きい値を1、それ以外を0にすればよい。  
即ち、  
  
    IMG = ORG>128;  
  
とする。  
2階調画像を図8に示す。  
  
![ex2_2](https://github.com/hid3kua0/tdu_image_processing/blob/master/kadaipic/ex2_2.png)  
  
図8　2階調画像  
  
原画像を4階調にするには、原画像の輝度値が256階調なので、これを4つに区切り、各閾値ごとに輝度値を変更すればよい。  
即ち、  
  
    IMG0 = ORG>64;  
    IMG1 = ORG>128;  
    IMG2 = ORG>192;  
    IMG = IMG0 + IMG1 + IMG2;  
  
とすればよい。  
4階調画像を図9に示す。  
  
![ex2_3](https://github.com/hid3kua0/tdu_image_processing/blob/master/kadaipic/ex2_3.png)  
  
図9　4階調画像  
  
原画像を8階調にするには、原画像の輝度値が256階調なので、これを8つに区切り、各閾値ごとに輝度値を変更すればよい。  
即ち、  
  
    IMG0 = ORG>32;  IMG1 = ORG>64;  IMG2 = ORG>96;  IMG3 = ORG>128;  
    IMG4 = ORG>160; IMG5 = ORG>192; IMG6 = ORG>224;  
    IMG = IMG0 + IMG1 + IMG2 + IMG3 + IMG4 + IMG5 + IMG6;  
  
とすればよい。  
8階調画像を図10に示す。  
  
![ex2_4](https://github.com/hid3kua0/tdu_image_processing/blob/master/kadaipic/ex2_4.png)  
  
図10　8階調画像  
   
このように、階調を上げるほど情報量が増え、画像が判り易くなる。  
   
   
課題3  
閾値を4パターン設定し,閾値処理した画像を示せ。  
   
設定した閾値は64, 96, 128, 192の4パターンである。   
即ち、  
  
    IMG = ORG > 64; % 輝度値が64以上の画素を1，その他を0に変換  
   
    IMG = ORG > 96;  
   
    IMG = ORG > 128;  
   
    IMG = ORG > 192;  
   
となる。  
閾値処理した各画像を図11から図14に示す。  
  
![ex3_1](https://github.com/hid3kua0/tdu_image_processing/blob/master/kadaipic/ex3_1.png)  
   
図11　閾値64の画像  
  
![ex3_2](https://github.com/hid3kua0/tdu_image_processing/blob/master/kadaipic/ex3_2.png)  
   
図12　閾値96の画像  
  
![ex3_3](https://github.com/hid3kua0/tdu_image_processing/blob/master/kadaipic/ex3_3.png)  
   
図13　閾値128の画像  
  
![ex3_4](https://github.com/hid3kua0/tdu_image_processing/blob/master/kadaipic/ex3_4.png)  
   
図14　閾値192の画像  
   
このように、閾値によって表現される情報が変わることが分かる。  
   
   
課題4  
画素の濃度ヒストグラムを生成せよ。  
  
    imhist(ORG); % ヒストグラムの表示  
   
により、濃度ヒストグラムを生成する。   
生成された濃度ヒストグラムを図15に示す。  
   
![ex4_1](https://github.com/hid3kua0/tdu_image_processing/blob/master/kadaipic/ex4_1.png)  
   
図15　濃度ヒストグラム  
   
このように、原画像は画素濃度が200から250付近に集中していることが分かる。   
   
   
課題5  
判別分析法を用いて画像を2値化せよ。  
  
判別分析法とは、対象物の濃度と背景の濃度とがそれぞれ最も良くまとまり、かつ対象物と背景との違いが際立つように閾値を定める方法。   
即ち、閾値tで画像を2つのクラスに分けたとき、その2つのクラス間分散の各クラス内分散に対する比の値が最も大きくなるように閾値tを定める。   
判別分析法を行うには、以下の処理を行う。  
  
    H = imhist(ORG); %ヒストグラムのデータを列ベクトルEに格納   
       
    myu_T = mean(H); %全画素の濃度平均値  
       
    max_val = 0;  
    max_thres = 1;  
       
    for i=1:255  
    C1 = H(1:i); %ヒストグラムを2つのクラスに分ける  
    C2 = H(i+1:256);  
        
    n1 = sum(C1); %画素数の算出   
    n2 = sum(C2);   
          
    myu1 = mean(C1); %平均値の算出   
    myu2 = mean(C2);  
       
    sigma1 = var(C1); %分散の算出  
    sigma2 = var(C2);  
       
    sigma_w = (n1 *sigma1+n2*sigma2)/(n1+n2); %クラス内分散の算出  
    sigma_B = (n1 *(myu1-myu_T)^2+n2*(myu2-myu_T)^2)/(n1+n2); %クラス間分散の算出  
       
    if max_val<sigma_B/sigma_w  
    max_val = sigma_B/sigma_w;  
    max_thres =i;  
    end;  
       
    end;  
   
上記のfor文内の処理をクラスの分割位置を少しずつ変えながら繰り返し行う。  
また、if文内でクラス間分散とクラス内分散の比が最大になる閾値を求める。  
   
    IMG = ORG > max_thres;  
   
により、求めた閾値で画像を生成する。   
生成された画像を図16に示す。  
   
![ex5_1](https://github.com/hid3kua0/tdu_image_processing/blob/master/kadaipic/ex5_1.png)  
   
図16　判別分析法による生成画像  
   
   
課題6   
画像を2値化せよ。  

2種類の方法を用いて原画像を2値化する。  

    IMG = ORG>128; % 128による二値化 
    imagesc(IMG); colormap(gray); colorbar; % 画像の表示 
   
により、中間値を閾値とした2値化を行う。  
128で2値化された画像を図17に示す。  
   
![ex6_1](https://github.com/hid3kua0/tdu_image_processing/blob/master/kadaipic/ex6_1.png)   
   
図17　128で2値化された画像   
   
    IMG = dither(ORG); % ディザ法による二値化 
    imagesc(IMG); colormap(gray); colorbar; % 画像の表示 
   
により、ディザ法を用いた2値化を行う。   
ディザ法で2値化された画像を図18に示す。   
   
![ex6_2](https://github.com/hid3kua0/tdu_image_processing/blob/master/kadaipic/ex6_2.png)  
   
図18　ディザ法で2値化された画像   
   
   
課題7   
画素のダイナミックレンジを０から２５５にせよ。      
   
ダイナミックレンジを0から255にするには、
   
    imhist(ORG); % 濃度ヒストグラムを生成、表示  
 
    ORG = double(ORG);  
    mn = min(ORG(:)); % 濃度値の最小値を算出  
    mx = max(ORG(:)); % 濃度値の最大値を算出  
    ORG = (ORG-mn)/(mx-mn)*255;  
    imagesc(ORG); colormap(gray); colorbar; % 画像の表示  
  
    ORG = uint8(ORG);   
    imhist(ORG); % 濃度ヒストグラムを生成、表示  
   
とすればよい。   
ダイナミックレンジを変える前の画像とヒストグラム、変えた後の画像とヒストグラムを図19から図22に示す。   
   
![ex7_1](https://github.com/hid3kua0/tdu_image_processing/blob/master/kadaipic/ex7_1.png)   
   
図19　ダイナミックレンジ変更前の画像   
   
![ex7_2](https://github.com/hid3kua0/tdu_image_processing/blob/master/kadaipic/ex7_2.png)   
   
図20　ダイナミックレンジ変更前のヒストグラム   
   
![ex7_3](https://github.com/hid3kua0/tdu_image_processing/blob/master/kadaipic/ex7_3.png)   
   
図21　ダイナミックレンジ変更後の画像   
   
![ex7_4](https://github.com/hid3kua0/tdu_image_processing/blob/master/kadaipic/ex7_4.png)   
   
図22　ダイナミックレンジ変更後のヒストグラム   
   
    ORG = uint8(ORG);
   
について、これは配列を8ビット符号なし整数へ変換する処理である。ダイナミックレンジが0から255の整数値である必要があるためこの処理を行う。   
   
   
課題8   
二値化された画像の連結成分にラベルをつけよ。   
   
2値化画像の連結成分にラベリングするには、   
   
    IMG = ORG > 128; % 閾値128で二値化   
   
を行い、   
   
    IMG = bwlabeln(IMG);
   
によりラベリングをすればよい。   
ラベリングされた画像を図23に示す。   
   
![ex8_2](https://github.com/hid3kua0/tdu_image_processing/blob/master/kadaipic/ex8_2.png)   
   
図23　ラベリングされた画像   
   
   
課題9   
メディアンフィルターを適用し，ノイズ除去を体験せよ。   
   
メディアンフィルタによるノイズ除去を行うには、   
   
    ORG = imnoise(ORG,'salt & pepper',0.02); % ノイズ添付   
   
    IMG = filter2(fspecial('average',3),ORG); % 平滑化フィルタで雑音除去   
   
    IMG = medfilt2(ORG,[3 3]); % メディアンフィルタで雑音除去   
   
    f=[0,-1,0;-1,5,-1;0,-1,0]; % フィルタの設計   
    IMG = filter2(f,IMG,'same'); % フィルタの適用   
   
とすればよい。   
ノイズ添付時、平滑化フィルタによる雑音除去時、メディアンフィルタによる雑音除去時、メディアンフィルタ適応時のそれぞれの画像を図24から図27に示す。   
   
![ex9_1](https://github.com/hid3kua0/tdu_image_processing/blob/master/kadaipic/ex9_1.png)   
   
図24　ノイズ添付時の画像   
   
![ex9_2](https://github.com/hid3kua0/tdu_image_processing/blob/master/kadaipic/ex9_2.png)   
   
図25　平滑化フィルタによる雑音除去時の画像   
   
![ex9_3](https://github.com/hid3kua0/tdu_image_processing/blob/master/kadaipic/ex9_3.png)   
   
図26　メディアンフィルタによる雑音除去時の画像   
   
![ex9_4](https://github.com/hid3kua0/tdu_image_processing/blob/master/kadaipic/ex9_4.png)   
   
図27　メディアンフィルタ適応時の画像   
   
   
課題10   
エッジ抽出を体験せよ。   
   
エッジ抽出における3つの方法を試す。   
   
    IMG = edge(ORG,'prewitt'); % エッジ抽出（プレウィット法）   
   
    IMG = edge(ORG,'sobel'); % エッジ抽出（ソベル法）   
   
    IMG = edge(ORG,'canny'); % エッジ抽出（キャニー法）   
   
により、それぞれプレウィット法、ソベル法、キャニー法によるエッジ抽出を行う。   
3つのエッジ抽出法により生成された画像を図28から図30に示す。   
   
![ex10_1](https://github.com/hid3kua0/tdu_image_processing/blob/master/kadaipic/ex10_1.png)   
   
図28　プレウィット法によるエッジ抽出   
   
![ex10_2](https://github.com/hid3kua0/tdu_image_processing/blob/master/kadaipic/ex10_2.png)   
   
図29　ソベル法によるエッジ抽出   
   
![ex10_3](https://github.com/hid3kua0/tdu_image_processing/blob/master/kadaipic/ex10_3.png)   
   
図30　キャニー法によるエッジ抽出   
   










