**Create two namespaces and connect with Veth**

**Step 1:** Create namespaces call “earth” and “jupyter”.

ip netns add earth

ip netns add jupyter

**To see all the namespaces enter the command:**

ip netns list

**Step 2:** Create veth pairs:

ip link add veth0 type veth peer name veth1

**Step 3:** Move one end of each veth pair to a namespace:

ip link set veth0 netns earth

ip link set veth1 netns jupyter

**Step 4:** Configure IP addresses:

ip netns exec earth ip addr add 192.168.1.1/24 dev veth0

ip netns exec jupyter ip addr add 192.168.1.2/24 dev veth1

**Step 5:** Bring up the interfaces:

ip netns exec earth ip link set dev veth0 up

ip netns exec jupyter ip link set dev veth1 up

**Check:**

ip netns exec earth ping 192.168.1.2

ip netns exec jupyter ping 192.168.1.1
