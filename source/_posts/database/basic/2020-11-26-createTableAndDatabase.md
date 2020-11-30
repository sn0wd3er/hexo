---
title: 데이터 베이스 및 테이블 만들기
date: 2020-11-26 16:00:06
tags:
- Database Query
category:
- Database
---

## 데이터 베이스 생성 및 테이블 만들기

```
CREATE DATABASE ModelDB;

USE ModelDB;

CREATE TABLE customerTBL(
	customerName NCHAR(3) NOT NULL,
	customerBirth INT NOT NULL,
	customerAddress NCHAR(2) NOT NULL,
	customerNumber CHAR(12),
	CONSTRAINT customerTBL_pk PRIMARY KEY(customerName) 
)

CREATE TABLE purchaseTBL(
	customerName NCHAR(3) NOT NULL,
	product NCHAR(3) NOT NULL,
	price INT NOT NULL,
	amount INT NOT NULL,
	CONSTRAINT purchaseTBL_fk FOREIGN KEY(customerName) REFERENCES customerTBL(customerName)
)

SELECT * FROM customerTBL;
SELECT * FROM purchaseTBL;

```

- `CREATE DATABASE [NAME]` : 데이터 베이스 생성
- `USE [DATABASE]` : 데이터 베이스 사용
- `CREATE TABLE [NAME](Column Name)` : 테이블 생성 후 Column이름과 데이터 형식 설정
- `CONSTRAINT [제약조건 이름] PRIMARY KEY(테이블 이름)` : 해당 되는 테이블 이름을 기본키로 설정
- `CONSTRAINT [제약조건 이름] FOREIGN KEY(테이블 이름) REFERNECES [테이블 이름](왜래키와 연결할 테이블이름)` : 외래키를 설정

- `SELECT [열 이름] FROM [테이블]` : 테이블 조회
