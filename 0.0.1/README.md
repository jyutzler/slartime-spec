# The SlarTime Format Specification

Authors:
  * Jeff Yutzler (Image Matters LLC)

## Abstract

`SlarTime` is an extension to [GeoJSON](http://geojson.org/) providing support for temporal values.

## Contents

  * 1\. [Introduction](#1-introduction)
    * 1.1. [Definitions](#11-definitions)
  * 2\. [Temporal Objects](#2-temporal-objects)
    * 2.1. [Type](#21-type)
    * 2.2. [Temporal Position](#22-temporal-position)
    * 2.3. [Instant](#21-type)
    * 2.4. [Period](#22-period)
    * 2.5. [Sequence](#23-sequence)
  * 3\. [Examples](#3-examples)

## 1. Introduction

This specification describes an extension to [GeoJSON](http://geojson.org/)
that specifies an encoding for temporal values as members of a GeoJSON Feature object.
As such, files implementing `SlarTime` are by
definition valid GeoJSON files and valid [JSON](http://json.org/) files.
`SlarTime` implements a subset of the temporal schema described in [ISO19108](http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=26013).
This subset was curated in order to support the most common temporal requirements including moving features and map stories. 

### 1.1. Definitions

JavaScript Object Notation (JSON), and the terms “object”, “name”, “value”, “array”, and “number”, are defined in [IETF RTC 4627](http://www.ietf.org/rfc/rfc4627.txt).

The key words “MUST”, “MUST NOT”, “REQUIRED”, “SHALL”, “SHALL NOT”, “SHOULD”, “SHOULD NOT”, “RECOMMENDED”, “MAY”, and “OPTIONAL” in this document are to be interpreted as described in [IETF RFC 2119](http://www.ietf.org/rfc/rfc2119.txt).

## 2. Temporal Objects

Feature objects within a GeoJSON object MAY have a member with the name `datetime` that describes a temporal aspect of the object.
Feature objects with a `datetime` member MUST conform to the requirements in this document.

### 2.1. Type

A `datetime` member MUST have a member named `type`. 
This member's value is a string that determines the type of temporal object.
The value of the `type` member MUST be one of the following strings:

   * "Instant"
   * "Period"
   * "Sequence"
   
The case of the `type` member values MUST be as shown here.

### 2.2. Temporal Position

A temporal position is the fundamental temporal construct. 
A `datetime` member MUST have a member named `positions`.
The structure of the value of this member MUST be an array of one or more temporal positions.
Temporal positions MUST be encoded as an [ISO-8601](http://www.iso.org/iso/home/standards/iso8601.htm) string.
The cardinality of the array MUST be determined by the `type` as described below.

### 2.3. Instant

For the type "Instant", the `positions` array MUST contain exactly one temporal position. 

### 2.4. Period

For the type "Period", the `positions` array MUST contain exactly two temporal positions. 
The first member of the array (index "0") MUST be the beginning of the period. 
The second member of the array (index "1") MUST be the end of the period.

### 2.5. Sequence

For the type "Sequence", the `positions` array MUST contain one or more temporal positions. 
The members of the array MUST be in chronological order from earliest to latest.

## 3. Examples

TBD
