---
title: "전북대학교 공지 모니터링 시스템"
description: "대학 공지사항 수집 및 맞춤형 알림 자동화 프로젝트"
date: 2026-09-15
showDate: false
showReadingTime: false
showWordCount: false
showAuthor: false
showViews: false
showLikes: false
showEdit: false
---

## Overview

<div class="project-overview">
  <table>
    <tbody>
      <tr><th scope="row">개발 기간</th><td>2026.09 ~ 현재</td></tr>
      <tr><th scope="row">진행 상태</th><td>개발 중</td></tr>
      <tr><th scope="row">개발 형태</th><td>개인 프로젝트</td></tr>
      <tr><th scope="row">사용 기술</th><td>Python, requests, BeautifulSoup, Git</td></tr>
      <tr><th scope="row">담당 역할</th><td>기획, 설계 및 개발</td></tr>
    </tbody>
  </table>
</div>

대학 홈페이지의 공지사항을 자동으로 수집하고, 사용자에게 필요한 정보를 선별해 전달하는 시스템을 개발하고 있습니다.

{{< project-card
  title="zichana1598 / jbnu-notice-monitor"
  tech="Python · requests · BeautifulSoup"
  url="https://github.com/zichana1598/jbnu-notice-monitor"
  icon="github"
  linkLabel="GitHub에서 소스 코드 보기"
>}}
공지사항 HTML 수집과 파싱, Notice 데이터 모델의 소스 코드를 확인할 수 있습니다.
{{< /project-card >}}

## Background

대학에서 제공하는 공지사항은 여러 게시판에 분산되어 있어 필요한 정보를 확인하려면 각 게시판을 직접 방문해야 합니다.

또한 공지마다 신청 대상과 마감일이 다르기 때문에, 단순히 새로운 공지가 올라왔는지 확인하는 것만으로는 자신에게 필요한 정보를 놓칠 수 있습니다.

이러한 문제를 해결하기 위해 공지 수집부터 중요도 판단, 알림까지 자동화하는 시스템을 기획했습니다.

## Goals

- 여러 게시판의 공지사항 자동 수집
- 신규 공지 감지 및 변경 이력 관리
- 신청 자격과 마감일을 고려한 중요도 분류
- Discord를 통한 맞춤형 알림 제공

## Architecture

### 기술 선택

Python은 HTTP 요청과 HTML 파싱을 위한 라이브러리를 활용하기 쉽고,
별도의 웹 서버 없이도 공지사항 수집 프로그램을 구현할 수 있어 선택했습니다.

- **requests** — 대학 홈페이지에 HTTP 요청을 보내 HTML 데이터를 수집
- **BeautifulSoup** — HTML 구조를 분석하여 공지 정보를 추출

### 구현 구조

현재 공지사항 수집과 데이터 변환 기능을 다음과 같은 구조로 구현했습니다.

<ol class="project-flow not-prose" role="list" aria-label="공지 데이터 처리 순서">
  <li class="project-flow__step">
    <strong class="project-flow__title">HTTP Collector</strong>
    <p>대학 홈페이지에서 HTML 수집</p>
    <span class="project-flow__arrow" aria-hidden="true">→</span>
  </li>
  <li class="project-flow__step">
    <strong class="project-flow__title">CSAI Parser</strong>
    <p>HTML에서 공지 정보 추출</p>
    <span class="project-flow__arrow" aria-hidden="true">→</span>
  </li>
  <li class="project-flow__step">
    <strong class="project-flow__title">Notice Model</strong>
    <p>추출한 정보를 공통 데이터 구조로 변환</p>
  </li>
</ol>

네트워크 통신과 HTML 파싱의 책임을 분리하여,
게시판 구조가 변경되거나 수집 대상을 확장할 때
각 기능을 독립적으로 수정할 수 있도록 구성했습니다.

## My Contribution

개인 프로젝트로 기획부터 구현까지 전반적인 작업을 진행하고 있습니다.

- 대학 공지 확인 과정에서 발생하는 불편함을 바탕으로 프로젝트 주제 선정
- 공지 수집, 신규 공지 감지, 중요도 분류 등 주요 기능과 개발 범위 결정
- 공지 수집과 데이터 변환을 분리하는 프로그램 구조 구성
- Python 기반 공지 목록 수집 및 파싱 기능 개발
- Git을 활용한 소스 코드 및 변경 이력 관리

프로젝트 진행 과정에서 AI 에이전트를 활용하여
기술 조사와 구현 작업을 보조받고 있습니다.

## Implementation

### 현재 구현한 기능

**공지사항 수집**

- HTTP 요청을 통한 대학 홈페이지 접근
- 공지사항 페이지의 HTML 데이터 수집

**공지 데이터 변환**

- 게시판 HTML에서 공지 정보 추출
- 추출한 정보를 공통 Notice 데이터 형식으로 변환

### 구현 과정

1. 대학 홈페이지의 공지 목록 구조 분석
2. HTTP 요청을 통한 HTML 수집 기능 구현
3. BeautifulSoup을 이용한 공지 정보 추출 기능 구현
4. 추출한 정보를 공통 Notice 데이터 구조로 변환
5. 수집과 파싱 기능을 연결하여 기본 처리 흐름 구성

현재는 공지 수집과 기본적인 데이터 변환까지 구현한 상태입니다.

## Roadmap

### 단기 목표

- SQLite를 활용한 공지 데이터 저장
- 기존 데이터와 비교하여 신규 공지 감지
- 수집 및 파싱 기능 테스트

### 장기 목표

- 공지 본문 및 첨부파일 분석
- 신청 자격과 마감일을 고려한 중요도 분류
- Discord 알림 기능 구현
- 수집 대상 게시판 확장

## Retrospective

### 현재까지의 경험

대학 공지사항을 자동으로 확인하고 싶다는 필요에서 시작한 프로젝트입니다.

개발을 진행하면서 공지사항을 단순히 수집하는 것과
실제로 필요한 정보를 사용자에게 전달하는 것은
서로 다른 문제라는 점을 확인했습니다.

특히 신청 대상과 마감일처럼 공지의 중요도를 판단하는 데
필요한 정보를 어떻게 처리할지가 중요한 과제로 남아 있습니다.

### 현재 한계와 개선 방향

현재는 단일 게시판의 공지 목록 수집과 파싱까지만 구현되어 있습니다.

우선 수집한 데이터를 저장하고 신규 공지를 감지하는 기능을 완성하여,
실제로 사용할 수 있는 최소한의 모니터링 시스템을 구축할 계획입니다.
