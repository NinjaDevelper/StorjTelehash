# Abstract Messaging Layer for Storj Platform

## About Abstract Messaging Layer
Massaging Layer in Storj Platform is used for communication between two
parties,  e.g. sending/receiving broadcast messages, negotiating 
service conditions, etc. Messaging layer is abstracted because many 
communication implemenations would be usable in Storj Platform. 
For now there is [telehash-c](https://github.com/telehash/telehash-c)
implementation for the underlying layer.

All messages are formated in JSON.

## Messages in  Messaging Layer
Every communications in messaging layer works in event-driven manner. i.e.
recievers must register handlers for them to act to received messages because
they don't know when messages come in. 
So there is no functions to send() and recv() directly.

### Channel Message

Channel message is used for general purpose. 
Recevier must register a handler as a channel handler with a channel name
if he want to act to a messages on the channel. Channel name is like a
_port number_ in TCP/IP, where receiver listen. At first the sender 
register a handler for responses and send a message 
with a channel name to a receiver. 
After sending messages, a reciever receives and read the message 
by a registered handler. When he wants to stop messaging, he would send
nothing.

### Handler for messages
Handler must implements ```Messaing.ChannelHander``` class. All methods that
starts with seq* would be run one by one when receiving messages.
The order of calling method is alphabeetic order.

## Example

The sample Python program  is below.

```python
from storj.messaging import ChannelHandler
from storjtelehash.storjtelehash import StorjTelehash

class ChannelOpener(ChannelHandler):
    """
    Channel handler for channel opener.
    Methods below would be called in alphabetic order.
    When you want to jump, e.g. to seqC(), use self.next = seqC
    When you want to call another ChannelHanlder instance, e.g. to handler,
    use self.call = handler
    """
    def seqA(self, packet):
        packet: recevied message 
        logging.debug('called by opener at 1st, i.e. when opening a  channel')
        return '{\"count\":0}'

    def seqB(self, packet):
        logging.debug('called by opener at 2nd')
        # packet would be '{\"count\":1}'
        #send back nothing.
        return None

    def seqC(self, packet):
    """
    never called
    """
        counter_opener = 9999
        return packet


class ChannelReceiver(ChannelHandler):
    """
    Channel handler for channel receiver.
    Methods below would be called in alphabetic order.
    """

    def seqA(self, packet):
        logging.debug('called by receiver at 1st')
        # packet would be '{\"count\":0}'
        return '{\"count\":1}'

    def seqB(self, packet):
        """
        never called
        """
        return packet

# initiate telehash as port=1234
s = StorjTelehash(1234)

# register channel handler with 'one_service' channel.
#register a Class, not an instance.
s.add_channel_handler('one_service', ChannelReceiver)

# open a channel with name 'another_service' with ChannelOpener handler.
#register an instnace, not a Class !
s.open_channel(locationB, 'another_service', ChannelOpener())
```
