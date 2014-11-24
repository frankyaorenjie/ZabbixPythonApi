ZabbixPythonApi
=================

Backgroud
-----------------

A simple way to connect to Zabbix api. It enables engineers to handle Zabbix resources more easily.

Examples
-----------------

```
zapi = ZabbixAPI(url='http://your.zabbix.address', user='admin', password='zabbix')
zapi.login()
print zapi.Graph.find({'graphid':'49931'}, attr_name='graphid')[0]
hostid = zapi.Host.find({'ip':ip}, attr_name='hostid')[0]
print zapi.Host.exists({'filter':{'host':'Zabbix-Proxy-Hostname'}})
host = zapi.createObject(Host, 'HostToCreate')
item = host.getItem('444107')
zapi.host.get({'hostids':['16913','17411'],'output':'extend'})
group = zapi.createObject(Hostgroup, '926')
print zapi.getHostByHostid('16913')
```

Update History
-------------------

### v1.0 - 24, Nov, 2014:

**Release notes:**

1. Remove test cases in zapi.py
2. Add use cases in `README.md`.

**TODO:**

1. Confirm the compatibility of higher version of zabbix.

### v0.5 - 24, May, 2012:

**Release notes:**

1. Fix bugs about list index problems.
2. Add some `try...except` to make code more robust.
3. Add method `find` to class `ZabbixAPIObjectFactory` for get data easily. This method will filter column of response and create missing object which you asked for. For example, if you want to get a template named `Template_Test` and api can not find it in Zabbix, method `find` will create it. So vilation for the response can be threw away. It can save a lot lines of code.
4. Completed `TODO 1` in `v0.4`. New scan_host(now named 'Spider' due to George RR Martin's great novel 'A Song of Ice and Fire').
5. Completed some frontend of Zabbix for its own php is hard to use and slow to load.
6. Add some readable excetions.

**TODO:**

1. Add more elements to Zabbix Platform(new frontend of Zabbix). According to the essential needs of work.

### v0.4 - 2, May, 2012:

**Release notes:**

1. Overwrite `__getattr__` in `ZabbixAPI` to make it dynamic to create Zabbix API object. No API objects unused will be created.
2. Add all API object to ZabbixAPI.
3. Abandon `TODO 1.` in `v0.3` because the attribues - mac and ip are connected to CMDB, not Zabbix. I move them to another CMDB API.
4. Abandon `TODO 4.` in `v0.3`. It will be a procedure as coding.
5. Completed `TODO 5.` in `v0.3`.

**TODO:**

1. To be considered later. I will use this API to refactor `scan_host` of Zabbix. Plus, `scan_host` is a script to add a host to Zabbix with its IP. And the script will add templates to the host according to the `netstat -ldunp` command and `ps -ef` command. This command can fetch process running on host and its port infomation is available.

### v0.3 - 20, Apr, 2012:

**Release notes:**

1. 'TODO 1.' postponed because connect to CMDB is in the first priority.
2. 'TODO 2.' improve relation between Host and Item.
3. Add staticmethod in ZabbixAPI 'zabbixGet' for get data remotely with 'zabbix_get'.

**TODO:**

1. Add Host attributes: mac address and ip address.
2. Doc.(long long long tern Oh, I'm so lazzzzzy)
3. Refactor with more design patterns.(long tern)
4. Make code more readable.
5. More readable exceptions.

### v0.2 - 15 Apr, 2012:

**Release notes:**

1. Complete `TODO 1.` in `v0.1`. Very thanks to gesheit. Now a factory class is used to make all api object with method `__getattr__`. Plus, a new decorator is made to act as a proxy for api object like `host`, `item` and etc,.
2. Copmplete `TODO 6.` in `v0.1`. Use teams' git for version control.

**TODO:**
1. Fullfill `ZabbixAPIObject`.
2. Research on the issue - relation among Resources.
3. Docs.(long long long tern Oh, I'm so lazzzzzy)
4. Refactor with more design patterns.(long tern)
5. Make code more readable.
6. More readable exceptions.
 
### v0.1 - 14 Apr, 2012:

**Release notes:**

1. Make framework for communication between script and web service.
2. Use decorator to POST/GET json and check users' auth.
3. Design patter 'Singleton' apply to main object(zapi in the example).
4. Two layers of objects - lower is called `ZabbixAPIObject` and the other is called `ZabbixObject`. `ZabbixAPIObject` is used to wrap json and `ZabbixObject` is the abstract of every RESOURCE(`host`, `item`, ...).
5. Use `exec` to define methods which is nearly alike in batch (every `ZabbixAPIObject` has a lot of methods which is nearly alike, only a word is different.(need to improved) 
6. Complete main `ZabbixObject` - `Host` and `Item` partly. They two is a sample of `ZabbixObject` relations. 

**TODO:**
1. Replace `exec` with other elegent method.
2. Fullfill `ZabbixAPIObject`.
3. Research on the issue - relation among Resources.
4. Doc.(long tern)
5. Refactor with more design patterns.(long tern)
6. Github.
7. More readable exceptions.
