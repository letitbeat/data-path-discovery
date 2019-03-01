# SDN Data-path Discovery

Docker compose file containing the services required to run the SDN Data-path discovery simulations.

## Services

* [ONOS][1] SDN Controller.
* [Data-plane emulator][2] Emulates a network topology and includes a network packet sniffer which is installed at all network interfaces of the data-plane forwarding devices, that forwards the traffic to the [analyzer][3].
* [Data-path analyzer][3] Tool that receives the packets, filters the packets having the UID and computes the flow trees from the set of observations.
* [UI][4] Web-based interface for discovering the data-paths that receives the interesting traffic to discover from the user and reports the resulting data-paths (in the form of a flow tree).
* [MongoDB][5] Database to store packets and data required by the [analyzer][3].
* [MongoDB Express][6] Web-based admin interface for MongoDB. *Optional*

### Prerequisites

* [Docker][7] Please refer to Docker [documentation][9] for detailed instructions on how to install it according to your platform.
* [Docker Compose][8] Once Docker is installed, you can proceed to [install][10] Docker Compose.

### How to run

Create and start the containers:
```
$ docker-compose up -d
```
Once the containers are started you can proceed to create the network topology and start the packet sniffer from within the data-plane container:

```
$ docker exec -it data-path-discovery_dp_1 bash
```

Inside the container execute:

```
$ python create_topology.py -a
```

To this point you should be able to visualize the topology and start using web interface at the following url:
`http://localhost:5000/`

### License

This project is licensed under the MIT License - see the [LICENSE.md][11] file for details

[1]: https://hub.docker.com/r/onosproject/onos/
[2]: https://github.com/letitbeat/dp-emulator
[3]: https://github.com/letitbeat/dp-analyzer
[4]: https://github.com/letitbeat/dpd-ui
[5]: https://hub.docker.com/_/mongo
[6]: https://hub.docker.com/_/mongo-express
[7]: https://www.docker.com
[8]: https://docs.docker.com/compose/
[9]: https://docs.docker.com/install/
[10]: https://docs.docker.com/compose/install/
[11]: https://github.com/letitbeat/data-path-discovery/blob/master/LICENSE