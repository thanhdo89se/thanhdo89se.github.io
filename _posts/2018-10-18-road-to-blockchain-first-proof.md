---
layout: post
title: "Road to Blockchain: The Lambda Chain"
comments: true
description: "Road to Blockchain - Triển khai mạng lưới Blockchain"
keywords: "blockchain, proofofstake, proofofwork, bitcoin, haskell, lambda, lmdb, cryptocyrrency, consensus"
---

Đối với một công việc nghiên cứu, ko có gì thú vị hơn khi được bắt đầu triển khai thực nghiệm đống lý thuyết "suông", để chứng minh rằng nó ko "suông".

Về blockchain, hiện tại có khá nhiều khoá học, mã nguồn mở, bài viết hướng dẫn xây dựng một mạng lưới blockchain đơn giản. Việc của bạn chỉ là bỏ một ít thời gian lướt github, udemy, đọc blog hay tham gia khoá học trực tiếp nếu dư dả là đã có thể tạo ra cho riêng mình một đồng "crypto coin" xịn xịn rồi.

Ở bài viết này, tôi mô tả lại những điểm mấu chốt trong việc khởi tạo một mạng blockchain, đơn sơ nhất. Nội dung bài viết ko phải là hướng dẫn "cài đặt" và "chạy" một hệ thống có sẵn như Solidity hay Hyperledger, mà là những kiến thức rất cơ bản về block, network, transaction... và cách xây dựng nên những thứ cơ bản đó.

---

## Core Modules

Ở 2 bài viết trước, chúng ta đã nắm được 3 đặc điểm quan trọng của blockchain là: Phân tán sổ cái, Toàn vẹn dữ liệu và Tự chủ hệ thống. Nếu quy ra công nghệ tương ứng, thì đó là: p2p-network, integrity-data, consensus-protocol.

Đó cũng chính là 3 thành phần quan trọng để bạn có thể đảm bảo mình đang xây dựng "blockchain network", chứ không phải là một thứ gì đó khác. Chi tiết thiết kế và thực thi từng module, bạn có thể xem ở url bên dưới.

List of lambda-chain core modules:

1.  [Peer-to-Peer Network](https://thanhdo89se.github.io/2018/road-to-blockchain-lambda-network/)

2.  [Integrity of Data](https://thanhdo89se.github.io/2018/road-to-blockchain-lambda-integrity-of-data)

3.  [PoW Consensus Protocol](https://thanhdo89se.github.io/2018/road-to-blockchain-lambda-consensus-protocol)

---

## Cryptocurrency

Khi đã hoàn thành xong một hệ thống Blockchain network đơn giản, hiểu về công nghệ nền tảng và khái niệm của blockchain, chúng ta tiếp tục thử nghiệm đưa các giao dịch tiền số vào blockchain, để tạo ra như một thứ nổi tiếng khác: Crytocurrency

Nội dung tiếp theo trong series là về transaction và wallet:

[lambdachain: Crytocurrency](https://thanhdo89se.github.io/2018/road-to-blockchain-lambda-cryptocurrency)

---

## Lambda Database - The lightnight

Hầu hết các chain lớn hiện tại đều sử dụng no-sql db, như level-db, rocks-db, có lẽ vì 2 lí do:

1. Cấu trúc dữ liệu và quan hệ giữa các loại dữ liệu ko phức tạp.

2. Bitcoin sử dụng level-db, nên nhiều chain thiết kế sau này cũng tham khảo theo.

Monero sử dụng LMDB, cũng là một dạng key-pair db, và tôi chọn LMDB cho lambda chain vì đã từng code trước đây.
Hơn nữa, lần setup và sử dụng LMDB gần đây, đã giúp tôi thu thập thêm kha khá kiến thức về IO, memory, channel.. rất hay và đáng để học hỏi.

Tôi dành một chapter trong series để viết về LMDB.

[Lambda-db - The Lightning Memory-Mapped Database](https://thanhdo89se.github.io/2018/lambda-db)

---

## Project Structure

[Source code của lambda-chain](https://github.com/thanhdo89se/lambda-chain) rất đơn giản, chỉ có vài file hs.

```haskell
-- data.mdb/
-- Network/
-- -- Connection.hs
-- -- Message.hs
-- -- Node.hs
-- Address.hs
-- Block.hs
-- Crypto.hs
-- Dash.hs
-- Persistence.hs
-- Transaction.hs
```
Đọc tên file là biết module đó làm gì rồi ha.

Thư mục `data.mdb`: nơi lưu trữ database, tạo bởi LMDB.

Một file có tên lạ lạ: `Dash.hs`, chính là CLI của program, vì tôi cũng ko biết nên đặt tên gì cho nó :)