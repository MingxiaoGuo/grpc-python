# grpc-python

* use `python3` command always
* open two `power shell`, one type `python3 server.py`, 当第一个shell打印出`init Server started at...3000`，在另外的shell里输入`python3 client.py`
* 如果server端报错，ctrl+c停止服务，调试成功再运行

1. server.py
  ```
      def encode(self, request, context):
        '''
        :return: encoder_pb2.EncodeResponse
        '''
        # TODO
        newId = 0
        myList = list(request.url)
        for i in range(0, len(myList)):
            if ('a' <= myList[i] and myList[i] <= 'z'):
              newId = newId * 62 + ord(myList[i]) - ord('a')
            if ('A' <= myList[i] and myList[i] <= 'Z'):
              newId = newId * 62 + ord(myList[i]) - ord('A') + 26
            if ('0' <= myList[i] and myList[i] <= '9'):
              newId = newId * 62 + ord(myList[i]) - ord('0') + 52
        print("Encode:\n", request)
        return encoder_pb2.EncodeResponse(id=newId)
  ```
2. client.py
  ```
      def decode(self, request, context):
        '''
        :return: encoder_pb2.DecodeResponse
        '''
        map = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789"
        result = ""
        count = request.id
        while (count > 0): 
            result += map[int(count%62)]
            count = int(count / 62)

        result = result[::-1] # reverse string
        print("Decode:\n", request)
        return encoder_pb2.DecodeResponse(url=result)
  ```
