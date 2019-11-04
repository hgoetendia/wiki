---
title: SMPP
description: Short message peer-to-peer 
published: true
date: 2019-11-04T05:32:08.262Z
tags: 
---

# Encoding & Languages

|     |Data Coding   |
|-------|-----------|
| 0x00  | GSM 7 bit encoding  |
| 0x01  | US-ASCII  |
|0x03   | ISO8859-1 (Latin-1), delivered as GSM-7 |
|0x04   | Binary  |
|0x08   | UCS-2 / UTF-16BE  |


https://smpp.io/encoding-lang/

http://angelaticalvarez.blogspot.com/2016/10/iso-8859.html

<table>
    <thead>
        <tr>
            <th>Layer 1</th>
            <th>Layer 2</th>
            <th>Layer 3</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td rowspan=4>L1 Name</td>
            <td rowspan=2>L2 Name A</td>
            <td>L3 Name A</td>
        </tr>
        <tr>
            <td>L3 Name B</td>
        </tr>
        <tr>
            <td rowspan=2>L2 Name B</td>
            <td>L3 Name C</td>
        </tr>
        <tr>
            <td>L3 Name D</td>
        </tr>
    </tbody>
</table>