# grpc-python

1. use `python3` command always
2. server.py
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
3. client.py
  coding...
