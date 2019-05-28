---
layout: post
title: Apple Pay in Swift
date: '2015-01-10 16:07:00'
tags:
- apple_pay
- ios
---

Apple Pay lets you use iPhone 6 and Apple Watch to pay in stores and apps in an easy, secure, and private way." 

Below method would be quick start for using this functionality in iOS8+ devices 

<table class="highlight tab-size-8 js-file-line-container" style="background-color: white; border-collapse: collapse; border-spacing: 0px; box-sizing: border-box; color: #333333; font-family: Helvetica, arial, freesans, clean, sans-serif, 'Segoe UI Emoji', 'Segoe UI Symbol'; font-size: 13px; line-height: 18.2000007629395px; tab-size: 8;">

<tbody style="box-sizing: border-box;">

<tr style="box-sizing: border-box;">

<td class="blob-code js-file-line" id="LC89" style="box-sizing: border-box; overflow: visible; padding: 0px 10px; position: relative; vertical-align: top;">/*   Method to make apple pay</td>

</tr>

<tr style="box-sizing: border-box;">

<td class="blob-code js-file-line" id="LC90" style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; overflow: visible; padding: 0px 10px; position: relative; vertical-align: top; white-space: pre;">*/</td>

</tr>

<tr style="box-sizing: border-box;">

<td class="blob-code js-file-line" id="LC91" style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; overflow: visible; padding: 0px 10px; position: relative; vertical-align: top; white-space: pre;">func applePaymentProcess(){</td>

</tr>

<tr style="box-sizing: border-box;">

<td class="blob-code js-file-line" id="LC95" style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; overflow: visible; padding: 0px 10px; position: relative; vertical-align: top; white-space: pre;">if(PKPaymentAuthorizationViewController.canMakePayments()){</td>

</tr>

<tr style="box-sizing: border-box;">

<td class="blob-code js-file-line" id="LC99" style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; overflow: visible; padding: 0px 10px; position: relative; vertical-align: top; white-space: pre;">let pkRequest = PKPaymentRequest();</td>

</tr>

<tr style="box-sizing: border-box;">

<td class="blob-code js-file-line" id="LC100" style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; overflow: visible; padding: 0px 10px; position: relative; vertical-align: top; white-space: pre;">pkRequest.countryCode = "US"</td>

</tr>

<tr style="box-sizing: border-box;">

<td class="blob-code js-file-line" id="LC101" style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; overflow: visible; padding: 0px 10px; position: relative; vertical-align: top; white-space: pre;">pkRequest.currencyCode = "USD"</td>

</tr>

<tr style="box-sizing: border-box;">

<td class="blob-code js-file-line" id="LC102" style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; overflow: visible; padding: 0px 10px; position: relative; vertical-align: top; white-space: pre;">pkRequest.supportedNetworks = [PKPaymentNetworkAmex,PKPaymentNetworkMasterCard,PKPaymentNetworkVisa]</td>

</tr>

<tr style="box-sizing: border-box;">

<td class="blob-code js-file-line" id="LC103" style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; overflow: visible; padding: 0px 10px; position: relative; vertical-align: top; white-space: pre;">pkRequest.merchantCapabilities = PKMerchantCapability.CapabilityEMV</td>

</tr>

<tr style="box-sizing: border-box;">

<td class="blob-code js-file-line" id="LC105" style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; overflow: visible; padding: 0px 10px; position: relative; vertical-align: top; white-space: pre;">// pkRequest.merchantIdentifier =</td>

</tr>

<tr style="box-sizing: border-box;">

<td class="blob-code js-file-line" id="LC107" style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; overflow: visible; padding: 0px 10px; position: relative; vertical-align: top; white-space: pre;">let item1 = PKPaymentSummaryItem.init(label:"motoX", amount:34.5)</td>

</tr>

<tr style="box-sizing: border-box;">

<td class="blob-code js-file-line" id="LC108" style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; overflow: visible; padding: 0px 10px; position: relative; vertical-align: top; white-space: pre;">let item2 = PKPaymentSummaryItem.init(label:"motoG", amount:30.5)</td>

</tr>

<tr style="box-sizing: border-box;">

<td class="blob-code js-file-line" id="LC110" style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; overflow: visible; padding: 0px 10px; position: relative; vertical-align: top; white-space: pre;">pkRequest.paymentSummaryItems = [item1,item2]</td>

</tr>

<tr style="box-sizing: border-box;">

<td class="blob-code js-file-line" id="LC112" style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; overflow: visible; padding: 0px 10px; position: relative; vertical-align: top; white-space: pre;">var paymentPane = PKPaymentAuthorizationViewController.init(paymentRequest:pkRequest)</td>

</tr>

<tr style="box-sizing: border-box;">

<td class="blob-code js-file-line" id="LC114" style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; overflow: visible; padding: 0px 10px; position: relative; vertical-align: top; white-space: pre;">}</td>

</tr>

<tr style="box-sizing: border-box;">

<td class="blob-code js-file-line" id="LC116" style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; overflow: visible; padding: 0px 10px; position: relative; vertical-align: top; white-space: pre;">} 

</td>

</tr>

</tbody>

</table>

Git Hub Project : https://github.com/prashanthmadi/Apply-Pay-Sample-App---Swift