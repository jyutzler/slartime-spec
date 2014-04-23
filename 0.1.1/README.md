# The SlarTime Format Specification

Authors:
  * Jeff Yutzler (Image Matters LLC)

## Abstract

A simple specification that extends [GeoJSON](http://geojson.org/)
to encode feature data with point geometries or non-geometric properties
that change over time. 

## Contents

  * 1\. [Introduction](#1-introduction)
    * 1.1. [Definitions](#11-definitions)
  * 2\. [Temporal Objects](#2-temporal-objects)
    * 2.1. [Type](#21-type)
    * 2.2. [Instant](#22-instant)
    * 2.3. [MultiInstant](#23-multiinstant)
  * 3\. [Implementation Guidance](#3-implementation-guidance)
  * 4\. [Example](#4-example)

## 1. Introduction

This specification describes a profile of [GeoJSON](http://geojson.org/)
that specifies an encoding for temporal values as members of a GeoJSON Feature object.
As such, files implementing `SlarTime` are by
definition valid GeoJSON files and valid [JSON](http://json.org/) files.
`SlarTime` implements a subset of the temporal schema described in [ISO19108](http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=26013).
This subset was curated in order to support the most common temporal requirements including moving features and map stories. 

### 1.1. Definitions

JavaScript Object Notation (JSON), and the terms “object”, “name”, “value”, “array”, and “number”, are defined in [IETF RTC 4627](http://www.ietf.org/rfc/rfc4627.txt).

The key words “MUST”, “MUST NOT”, “REQUIRED”, “SHALL”, “SHALL NOT”, “SHOULD”, “SHOULD NOT”, “RECOMMENDED”, “MAY”, and “OPTIONAL” in this document are to be interpreted as described in [IETF RFC 2119](http://www.ietf.org/rfc/rfc2119.txt).

## 2. Temporal Objects

Feature objects within a GeoJSON object MAY have a member with the name `when` that describes a temporal aspect of the feature.
Feature objects with a `when` member MUST conform to the requirements in this document.

### 2.1. Type

A `when` member MUST have a member named `type`. 
This member's value is a string that determines the type of temporal object.
The value of the `type` member MAY be one of the following strings:

   * "MultiInstant"
   
The case of the `type` member values MUST be as shown here.

### 2.2. Instant

An instant is the fundamental temporal construct. 
Instants SHOULD be encoded as an [ISO-8601](http://www.iso.org/iso/home/standards/iso8601.htm) string 
unless otherwise noted. 
Instants SHOULD conform to the profile found in [RFC 3339](http://www.ietf.org/rfc/rfc3339.txt).

### 2.3. MultiInstant

For the type "MultiInstant", the `when` member MUST have a member named `instants`.
The `instants` member MUST be an array containing one or more instants. 
The members of the array MUST be in chronological order from earliest to latest.

## 3. Implementation Guidance
### 3.1. Features That Change Over Time
When a feature changes over time, 
the instants corresponding to the change or observation SHOULD be encoded as a MultiInstant.

### 3.2. Moving Features
When a feature has a point geometry that changes over time, 
the points SHOULD be encoded as a MultiPoint. 
The array indexes of the points and instants SHOULD be aligned.

### 3.3. Features with Changing Properties
When a feature has one or more non-geometric properties that changes over time, 
the properties SHOULD be encoded as arrays. 
The array indexes of the property elements and instants SHOULD be aligned.

## 4. Example

```
{ "type": "FeatureCollection",
    "features": [
      { "type": "Feature",
         "geometry": {
           "type": "MultiPoint",
           "coordinates": [
             [100.0, 0.0], [101.0, 0.0], [101.0, 1.0],
               [100.0, 1.0], [100.0, 0.0] ]
         },
        "when": {
           "type": "MultiInstant", 
           "instants": ["2010-04-08T14:24:32.117Z", "2011-05-08T14:24:32.117Z", 
                         "2012-06-08T14:24:32.117Z", "2013-07-08T14:24:32.117Z",
                         "2014-04-08T14:24:32.117Z"]},
         "properties": {
           "prop0": "value0",
           "prop1": {"this": "that"}
           }
      },
      { "type": "Feature",
         "geometry": {
           "type": "Point",
           "coordinates": [100.0, 0.0]
         },
        "when": {
           "type": "MultiInstant", 
           "instants": ["2010-04-08T14:24:32.117Z", "2011-05-08T14:24:32.117Z", 
                         "2012-06-08T14:24:32.117Z", "2013-07-08T14:24:32.117Z",
                         "2014-04-08T14:24:32.117Z"]},
         "properties": {
           "ChangingProp": [3,5,8,13,21]
         }
      }
    ]
}
```
