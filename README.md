# DPDK Packet Info

## Описание

Программа является модификацией примера базовой пересылки (простой каркасный пример приложения пересылки) из фреймворка DPDK.

Эта программа была изменена для чтения сетевого трафика из файла PCAP и отображения информации о пакетах уровней OSI 2, 3 и 4.
Эта программа не пересылает пакеты, как пример каркаса DPDK, а отбрасывает их.
Программа показывает только информацию из TCP/UDP-пакетов IPv4.
Для получения дополнительной информации: https://doc.dpdk.org/guides/sample_app_ug/skeleton.html


## Требования к программе
* Среда Linux
* Установленная библиотека libpcap
* Установленная версия фреймворка DPDK 23.11 в среде Linux
* Зарезервирована память для huge pages
* По крайней мере, 1 привязанный порт, совместимый с DPDK

## Компиляция программы
Программа имеет Makefile и рекомендуется компилировать программу с правами администратора. Пример для Ubuntu/Debian:
   ```
    $ sudo make
   ```

## Запуск программы
Программу следует запускать с правами администратора. Пример запуска программы в среде Linux:
   ```
      $ sudo ./build/basicfwd -l 1 -n 2 \ --vdev 'net_pcap0,rx_pcap=path/to/file/file_rx.pcap'
   ```

Где:

* -l <список ядер>: Список ядер для выполнения
* -n <количество каналов>: Установите количество используемых каналов памяти
* --vdev 'net_pcap0,rx_pcap=path/to/file/file_rx.pcap':
Устройства на основе PCAP создаются с использованием виртуального устройства опции –vdev. Имя устройства должно начинаться с префикса net_pcap, за которым следуют цифры или буквы. Имя уникально для каждого устройства. Если не указывать tx_pcap или tx_iface, vdev отбрасывает все пакеты на tx.

* Программу можно закрыть, используя Ctrl-C

## Пример вывода
```
EAL: Detected CPU lcores: 6
EAL: Detected NUMA nodes: 1
EAL: Detected shared linkage of DPDK
EAL: Multi-process socket /var/run/dpdk/rte/mp_socket
EAL: Selected IOVA mode 'PA'
EAL: VFIO support initialized
EAL: Probe PCI driver: net_virtio (1af4:1041) device: 0000:01:00.0 (socket -1)
eth_virtio_pci_init(): Failed to init PCI device
EAL: Requested device 0000:01:00.0 cannot be used
EAL: Probe PCI driver: net_e1000_em (8086:10d3) device: 0000:02:00.0 (socket -1)
TELEMETRY: No legacy callbacks, legacy socket not created
Port 0 MAC: 52 54 00 ca 26 9c

Core 1 forwarding packets. [Ctrl+C to quit]
Packet 55:
  L2: Destination MAC: 01:00:5e:7f:ff:fa
       Source MAC: 52:54:00:92:a4:7c
  L3: Source IP: 192.168.122.1
      Destination IP: 239.255.255.250
  L4: UDP: Source port: 51604
          Destination port: 1900
Packet 57:
  L2: Destination MAC: 01:00:5e:7f:ff:fa
       Source MAC: 52:54:00:92:a4:7c
  L3: Source IP: 192.168.122.1
      Destination IP: 239.255.255.250
  L4: UDP: Source port: 51604
          Destination port: 1900
Packet 58:
  L2: Destination MAC: 01:00:5e:7f:ff:fa
       Source MAC: 52:54:00:92:a4:7c
  L3: Source IP: 192.168.122.1
      Destination IP: 239.255.255.250
  L4: UDP: Source port: 51604
          Destination port: 1900
Packet 60:
  L2: Destination MAC: 01:00:5e:7f:ff:fa
       Source MAC: 52:54:00:92:a4:7c
  L3: Source IP: 192.168.122.1
      Destination IP: 239.255.255.250
  L4: UDP: Source port: 51604
          Destination port: 1900
```

## Демонстрационное видео
https://disk.yandex.ru/i/Wupt9BasmiMjoA