---
title : PHP III (PHP's Infernal Internal Index)
permalink/url: php-internal-index
date: 04/02/2015
tags: [coding, php, work]
description: Confounded php Arrays
---

 Recently I was debugging some confounded PHP code, and came across an error when trying to get something back from an array:

    $services = [array('service'=>'Car Wash'),
                 array('service'=>'Dork Library'),
                 array('service'=>'Pet bnb')];

    foreach($services as $service_index => $service){
        print_r($service);
        // Remove any Car wash service
        if($service['service'] == 'Car Wash'){
            unset($services[$service_index]);
        }
    }

    print_r($services[0]); // No output?!!?!?

Why doesn't `$services[0]` return anything?

As someone who doesn't use php much, this was confusing. I assumed that if you [destory the variable](http://php.net/manual/en/function.unset.php) here, then this means the next variable in line would of course be returned. But no, php has something much more devious, an internal array. Going through [the details of this](http://nikic.github.io/2012/03/28/Understanding-PHPs-internal-array-implementation.html) can get to *O(*C language*)* intensity. Basically the resolution to this gotacha is using:

    reset($services);   // Fixes the index on this array
    current($services); // Calls the item at the currently internal index,
                        // defaults to the first index