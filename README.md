# Doc2vec Sentiment Analysis

Sự thành công của Word2vec đã được chứng minh trong rất nhiều công trình NLP.

Nhắc lại về Word2vec, nó sử dụng 1 tập copus, qua một mạng Neural biểu diễn các word thành các vector, các vector giữ lại được tính chất ngữ nghĩa. Tức các từ mang ý nghĩa similar với nhau thì gần nhau trong không gian vector. Trong NLP, đây một trong những phương thức của word embedding. Word2vec hiện nay được sử dụng hết sức rộng rãi.

Với Doc2vec, ngoài từ (word), ta còn có thể biểu diễn các câu (sentences) thậm chí 1 đoạn văn bản (document). Khi đó, bạn có thể dễ dàng vector hóa cả một đoạn văn bản thành một vector có số chiều cố định và nhỏ, từ đó có thể chạy bất cứ thuật toán classification cơ bản nào trên các vector đó.

Trong notebook này, mình sẽ giới thiệu rất cơ bản basic concept để các bạn có thể hình dung Sentiment sử dụng Doc2vec như thế nào.

# Doc2vec

Doc2vec được giới thiệu bởi Google ([https://arxiv.org/pdf/1507.07998v1.pdf](https://arxiv.org/pdf/1507.07998v1.pdf)), cũng như Word2vec, có 2 model chính là: **DBOW** và **DM**

*  **DBOW** (distributed bag of words): Mô hình này đơn giản là không quan tâm thứ tự các từ, training nhanh hơn, không sử dụng local-context/neighboring. Mô hình chèn thêm 1 "word" là ParagraphID, ParagraphID này đại diện cho văn bản được training. Sau khi training xong có thể hiểu các vector ParagraphID này là vector embedded của các văn bản. Hình ảnh được mô tả trong bài báo:

![DBOW](doc2vec_dbow.jpg)

* **DM** (distributed memory): xem một paragraph là một từ, sau đó nối từ này vào tập các từ trong câu. Trong quá trình training, vector của paragraph và vector từ đều được update.

![DM](doc2vec_dm.jpg)


Tóm lại: ta xem văn bản như là một từ, docID/paragraphID được biểu diễn dạng 1-hot, được embedded vào không gian vector.

# Classification

Có được các vector văn bản từ `Gensim` package. Từ đây bạn có thể sử dụng bất cứ thuật toán phân lớp nào, bạn có thể thực hiện tiếp bước model selection đến khi nào đạt kết quả tốt nhất. Ở đây mình sử dụng `Logistic Regression` và `SVM`, hai thuật toán phân lớp đều cho kết quả khá tốt. 

**Accuracy 0.86376**

Confusion matrix, without normalization

![Confusion Matrix Logistic Regression](confusion_matrix_LR.png)
