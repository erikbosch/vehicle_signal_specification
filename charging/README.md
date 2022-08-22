# Temporary folder for charging expert group work

## Introduction

This document describes a possible way forward for handling of extension of charging-related data. Data is added either to the [Charging Station specification](ChargingStation.vspec)
in this folder or to the existing VSS data tree. Information in this folder might be moved to a different repository later.

## General Idea and Scope

Data that is specific to a particular vehicle is stored in the exisiting Vehicle tree. This is regardless of whether the data is calculated within the vehicle or calculated by backend.
Data that rather concerns the charging station is proposed to be in a separate tree.