# Highly Available and Auto-Scalable Magento Cluster

Get the highly available and scalable clustered solution for Magento - an extremely popular open source e-commerce platform. The given implementation ensures tracking and distribution of the incoming load, with automatic adjusting of the allocated resources amount according to it.

##Highlights
This JPS package automatically deploys Magento 2 to the environment, which initially contains 2 balancers, 2 application servers, 2 MySQL databases, 2 Memcached and 1 Storage containers. Herewith, we provide two cluster version for you to choose the most suitable one according to your preferences:
- run on PHP 5.6 version with a pair of replicated MySQL instances (master-master)
- run on PHP 7 version, with 1 DB instance to process requests and 1 more slave one for backups

##Environment Topology
![Cluster Topology](images/magento-cluster-topology.png)

###Specifics
 Layer | Server          | Number of CTs <br/> by default | Cloudlets per CT <br/> (reserved/dynamic) | Options
-------|-----------------| :-----------------------------:|:-----------------------------------------:|:-----:
LB     | Varnish(+Nginx 443 port)|           2                    |          1/8                               |   -
AS     | Nginx (PHP-FPM) |            2                   |         1/8                                |  -
DB     |      MySQL      |          2                     |          1/8                               |  -
CH     |     Memcached   |           2                    |         1/8                                |-
ST     |  Shared Storage |          1                     |           1/8                              |   -

* LB - Load balancer
* AS - Application server
* DB - Database
* CH - Cache
* ST - Shared Storage
* CT - Container

**Magento Version**: 2.0.4<br/>
**Varnish Version**: 4.1.1<br/>
**Nginx Version**: 1.8.0<br/>
**Php Version**: PHP 5.6.20 / PHP 7<br/>
**MySQL Database**: 5.6.31<br/>
**Memcached Version**: 1.4.15

### Additional functionality:
* pair of MySQL databases with either configured asynchronous master-master replication (within PHP 5.6.20-based solution) or extra slave DB instance for backups (within PHP 5.7-based solution);
* horizontal scaling enabled on compute nodes by CPU load. New AppServer will be added while 70% loading;
* failover sql connection between MySQL and CP nodes based on [mysqlnd_ms](http://php.net/manual/ru/book.mysqlnd-ms.php) plugin;
* Memcached HA for session storage.

---

## Deployment

### Public Cloud

In order to get this solution instantly deployed, click the "Deploy to Jelastic" button, specify your email address within the widget, choose one of the [Jelastic Public Cloud providers](https://jelastic.cloud) and press Install.

For PHP 5.6-powered version with asynchronous MySQL master-master replication:

[![Deploy](https://github.com/jelastic-jps/git-push-deploy/raw/master/images/deploy-to-jelastic.png)](https://jelastic.com/install-application/?manifest=https%3A%2F%2Fraw.githubusercontent.com%2Fjelastic-jps%2Fmagento%2Fmaster%2Fmagento-cluster%2Fphp5.6-manifest.jps) 

For PHP 7-powered version with additional slave MySQL instance for backups:

[![Deploy](https://github.com/jelastic-jps/git-push-deploy/raw/master/images/deploy-to-jelastic.png)](https://jelastic.com/install-application/?manifest=https%3A%2F%2Fraw.githubusercontent.com%2Fjelastic-jps%2Fmagento%2Fmaster%2Fmagento-cluster%2Fphp7-manifest.jps)

### Private Cloud 
To deploy the required package to Jelastic Private Cloud, import the required JPS manifest (see them above within repo files) via your dashboard ([detailed instruction](https://docs.jelastic.com/environment-export-import#import)).

### Add To Website
More information about installation widget for your website can be found in the [Jelastic JPS Application Package](https://github.com/jelastic-jps/jpswiki/wiki/Jelastic-JPS-Application-Package) reference.
