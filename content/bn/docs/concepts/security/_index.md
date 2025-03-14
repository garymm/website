---
title: "নিরাপত্তা"
weight: 85
description: >
  ক্লাউড-নেটিভ ওয়ার্কলোডকে নিরাপত্তা রক্ষা করার প্রস্তুতির জন্য ধারণাগুলি।
simple_list: true
---

এই কুবারনেটিস ডকুমেন্টেশনের এই অংশের উদ্দেশ্য আপনাকে ক্লাউড-নেটিভ প্রযুক্তিতে
নিরাপত্তামুলকভাবে ওয়ার্কলোডগুলি পরিচালনা শেখানোর সাহায্য করা এবং একটি কুবারনেটিসের ক্লাস্টার
নিরাপত্তামুলকভাবে রাখার গুরুত্বপূর্ণ দিক সম্পর্কে জানানো।

কুবারনেটিস ক্লাউড-নেটিভ স্থাপত্যের উপর ভিত্তি করে এবং ক্লাউড-নেটিভ তথ্য নিরাপত্তা সম্পর্কে ভাল অনুশীলনের
জন্য {{< glossary_tooltip text="CNCF" term_id="cncf" >}} থেকে 
পরামর্শ প্রদান করে।

আপনার ক্লাস্টার এবং অ্যাপ্লিকেশনগুলিকে কীভাবে সুরক্ষিত করবেন 
সে সম্পর্কে বিস্তৃত প্রেক্ষাপটের জন্য
[ক্লাউড নেটিভ নিরাপত্তা এবং কুবারনেটিস](/bn/docs/concepts/security/cloud-native-security/) পড়ুন।

## কুবারনেটিসের নিরাপত্তা ব্যবস্থা {#security-mechanisms}

কুবারনেটিসের মধ্যে বেশ কয়েকটি API এবং নিরাপত্তা কন্ট্রোল রয়েছে,
সেইসাথে [পলিসিগুলি](#পলিসি) সংজ্ঞায়িত করার উপায় যা আপনি কীভাবে তথ্য সুরক্ষা পরিচালনা করেন তার অংশ গঠন করতে পারে।

### কন্ট্রোল প্লেন সুরক্ষা

কোন কুবারনেটিসের ক্লাস্টারের জন্য একটি প্রধান নিরাপত্তা ব্যবস্থা হলো
[কুবারনেটিস API-এ অ্যাক্সেস কন্ট্রোল ](bn/docs/concepts/security/controlling-access) করা।

কুবারনেটিস আশা করে যে আপনি কন্ট্রোল প্লেনের মধ্যে এবং কন্ট্রোল প্লেন এবং এর ক্লায়েন্টদের মধ্যে
[ট্রানজিটে ডেটা এনক্রিপশন](/bn/docs/tasks/tls/managing-tls-in-a-cluster/)
প্রদান করতে TLS কনফিগার করবেন এবং ব্যবহার করবেন। আপনি কুবারনেটিস কন্ট্রোল প্লেনের মধ্যে
সংরক্ষিত ডেটার জন্য [এনক্রিপশন এট রেস্ট(encryption at rest)](/bn/docs/tasks/administer-cluster/encrypt-data/) সক্ষম করতে পারেন;
এটি আপনার নিজের ওয়ার্কলোডের ডেটার জন্য এনক্রিপশন এট রেস্ট ব্যবহার করা থেকে আলাদা,
যা একটি ভাল আইডিয়াও হতে পারে

### সিক্রেট

[সিক্রেট](/bn/docs/concepts/configuration/secret/) API কনফিগারেশন ভ্যালুগুলির জন্য মৌলিক
সুরক্ষা প্রদান করে যার জন্য গোপনীয়তা প্রয়োজন ।

### ওয়ার্কলোড সুরক্ষা

পড এবং তাদের কন্টেনারগুলি যথাযথভাবে আইসোলেট নিশ্চিত করতে
[পড নিরাপত্তা স্ট্যান্ডার্ডস](/bn/docs/concepts/security/pod-security-standards/)
আপনার প্রয়োজন হলে কাস্টম আইসোলেশন নির্ধারণ করার জন্য আপনি
[RuntimeClasses](/bn/docs/concepts/containers/runtime-class) ব্যবহার করতে পারেন।

[নেটওয়ার্ক পলিসি](/bn/docs/concepts/services-networking/network-policies/) আপনাকে 
পডগুলির মধ্যে, অথবা আপনার ক্লাস্টারের বাইরের নেটওয়ার্ক মধ্যে নেটওয়ার্ক ট্রাফিক নিয়ন্ত্রণ করতে দেয়।

আপনি পড, তাদের কন্টেনারগুলি এবং তাদের মধ্যে চলা ইমেজগুলির চারপাশে প্রতিরোধমূলক বা ডিটেক্টিভ
কন্ট্রোলগুলি প্রয়োগ করতে বিস্তৃত ইকোসিস্টেম থেকে সিকিউরিটি কন্ট্রোল স্থাপন করতে পারেন ।

### অডিটিং

কুবারনেটিস [অডিটিং লগিং](/bn/docs/tasks/debug/debug-cluster/audit/) একটি নিরাপত্তা-সংশ্লিষ্ট,
সময়ানুক্রমিক সেট অফ রেকর্ড সরবরাহ করে যা ক্লাস্টারের ক্রিয়াকলাপের অনুক্রমিক ডকুমেন্ট করে। ক্লাস্টার 
ব্যবহারকারীদের দ্বারা উত্পন্ন ক্রিয়াকলাপ, কুবার্নিটিস API ব্যবহার করা অ্যাপ্লিকেশন এবং নিয়ন্ত্রণ প্লেন নিজস্ব
ক্রিয়াকলাপগুলি অডিট করে।

## ক্লাউড প্রোভাইডার নিরাপত্তা

{{% thirdparty-content vendor="true" %}}

আপনি যদি আপনার নিজের হার্ডওয়্যার বা অন্য কোনো ক্লাউড প্রোভাইডার এ একটি কুবারনেটিস ক্লাস্টার চালান,
তাহলে নিরাপত্তার সর্বোত্তম অনুশীলনের জন্য আপনার ডকুমেন্টেশনের সাথে পরামর্শ করুন।
এখানে কিছু জনপ্রিয় ক্লাউড প্রোভাইডার এর নিরাপত্তা ডকুমেন্টেশনের লিঙ্ক রয়েছে :

{{< table caption="ক্লাউড প্রদায়কের নিরাপত্তা" >}}

IaaS প্রদায়ক        | লিঙ্ক |
-------------------- | ------------ |
আলিবাবা ক্লাউড | https://www.alibabacloud.com/trust-center |
আমাজন ওয়েব সার্ভিস | https://aws.amazon.com/security |
গুগল ক্লাউড প্ল্যাটফর্ম | https://cloud.google.com/security |
হুয়াওয়ে ক্লাউড | https://www.huaweicloud.com/intl/en-us/securecenter/overallsafety |
আইবিএম ক্লাউড | https://www.ibm.com/cloud/security |
মাইক্রোসফট আজওর | https://docs.microsoft.com/en-us/azure/security/azure-security |
অরাকেল ক্লাউড ইন্ফ্রাস্ট্রাকচার | https://www.oracle.com/security |
টেনসেন্ট ক্লাউড | https://www.tencentcloud.com/solutions/data-security-and-information-protection |
ভিএমওয়্যার ভিস্ফিয়ার | https://www.vmware.com/solutions/security/hardening-guides |

{{< /table >}}

## পলিসি

আপনি কুবারনেটিস-নেটিভ মেকানিজম ব্যবহার করে নিরাপত্তা পলিসি নির্ধারণ করতে পারেন,
যেমন [NetworkPolicy](/bn/docs/concepts/services-networking/network-policies/)
(নেটওয়ার্ক প্যাকেট ফিল্টারিং উপর ঘোষণামূলক কন্ট্রোল) বা
[ValidatingAdmissionPolicy](/bn/docs/reference/access-authn-authz/validating-admission-policy/)
(কুবারনেটিস API ব্যবহার করে কেউ কী পরিবর্তন করতে পারে তার ঘোষণামূলক সীমাবদ্ধতা)।

তবে, আপনি কুবারনেটিস পরিবেশের চারপাশে পলিসি কার্যান্বয়নে নির্ভর করতে পারেন। কুবারনেটিস এক্সটেনশন মেকানিজম সরবরাহ করে
এই পরিবেশ প্রকল্পগুলির উপর তাদের নিজস্ব পলিসি নিয়ন্ত্রণ সাধারণের জন্য
উন্মোচনের সুযোগ প্রদান করতে। এগুলি উদাহরণ হিসেবে উল্লেখ করা যেতে পারে:
সোর্স কোড পর্যালোচনা, কন্টেনার ইমেজ অনুমোদন, এপিআই অ্যাক্সেস নিয়ন্ত্রণ,
নেটওয়ার্কিং, এবং অন্যান্য।

পলিসি মেকানিজম এবং কুবারনেটিসের সম্পর্কে আরও তথ্য জানতে,
[পলিসি](/bn/docs/concepts/policy/) পড়ুন।

## {{% heading "whatsnext" %}}

সম্পর্কিত কুবারনেটিস নিরাপত্তা বিষয়গুলি জানুন:

* [আপনার ক্লাস্টার নিরাপত্তা সুরক্ষা করা](/bn/docs/tasks/administer-cluster/securing-a-cluster/)
* [পরিচিত দুর্বলতা](/bn/docs/reference/issues-security/official-cve-feed/)
  কুবারনেটিসে (এবং আরও তথ্যের লিঙ্ক)
* [ট্রানজিটে ডেটা এনক্রিপশন](/bn/docs/tasks/tls/managing-tls-in-a-cluster/) কন্ট্রোল প্লেনের জন্য
* [ডেটা এনক্রিপশন এট রেস্ট](/bn/docs/tasks/administer-cluster/encrypt-data/)
* [কুবারনেটিস API অ্যাক্সেস নিয়ন্ত্রণ](/bn/docs/concepts/security/controlling-access)
* [নেটওয়ার্ক পলিসি](/bn/docs/concepts/services-networking/network-policies/) পড এর জন্য
* [কুবারনেটিসে সিক্রেট](/bn/docs/concepts/configuration/secret/)
* [পডগুলির নিরাপত্তা স্ট্যান্ডার্ডস](/bn/docs/concepts/security/pod-security-standards/)
* [RuntimeClasses](/bn/docs/concepts/containers/runtime-class)

প্রসঙ্গ জানুন:

<!-- if changing this, also edit the front matter of content/en/docs/concepts/security/cloud-native-security.md to match; check the no_list setting -->
* [ক্লাউড নেটিভ নিরাপত্তা এবং কুবারনেটিস](/bn/docs/concepts/security/cloud-native-security/) পড়ুন।

সার্টিফাইড:

* [সার্টিফাইড কুবারনেটিস নিরাপত্তা বিশেষজ্ঞ](https://training.linuxfoundation.org/certification/certified-kubernetes-security-specialist/)
  সার্টিফিকেশন এবং অফিসিয়াল প্রশিক্ষণ কোর্স।

এই অধ্যায়ে আরো পড়ুন:

