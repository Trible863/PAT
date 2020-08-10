# PAT
1022 Digital Library
class Book:
    def __init__(self, num, title, author, keys, publisher, year):
        self.num = num
        self.title = title
        self.author = author
        self.keys = keys.copy()
        self.publisher = publisher
        self.year = year


def main():
    N = int(input().strip())
    book = []
    dic = [{} for _ in range(4)]  # title, author, key, publisher
    for i in range(N):
        num = int(input().strip())
        title = input().strip()
        if title not in dic[0]:
            dic[0][title] = len(dic[0])
        title = dic[0][title]

        author = input().strip()
        if author not in dic[1]:
            dic[1][author] = len(dic[1])
        author = dic[1][author]

        keys = input().strip().split()
        temp = []
        for key in keys:
            if key not in dic[2]:
                dic[2][key] = len(dic[2])
            key = dic[2][key]
            temp.append(key)
        keys = temp.copy()
        keys.sort()

        publisher = input().strip()
        if publisher not in dic[3]:
            dic[3][publisher] = len(dic[3])
        publisher = dic[3][publisher]

        year = int(input().strip())
        book.append(Book(num, title, author, keys, publisher, year))
    M = int(input().strip())
    for i in range(M):
        line = input().strip()
        print(line)  # 输出查询信息
        num = int(line[0])
        line = line.split(':')
        records = []
        if num <= 4:
            if line[1].strip() in dic[num - 1]:
                message_num = dic[num - 1][line[1].strip()]  # 代码编号
            else:
                print('Not Found')
                continue
            if num == 1:  # title
                for j in range(len(book)):
                    if book[j].title == message_num:
                        records.append(book[j].num)
            elif num == 2:  # author
                for j in range(len(book)):
                    if book[j].author == message_num:
                        records.append(book[j].num)
            elif num == 3:  # key
                for j in range(len(book)):
                    if message_num in book[j].keys:
                        records.append(book[j].num)
            else:
                for j in range(len(book)):
                    if book[j].publisher == message_num:
                        records.append(book[j].num)
        else:
            message_num = int(line[1].strip())
            for j in range(len(book)):
                if book[j].year == message_num:
                    records.append(book[j].num)
        if len(records) == 0:
            print('Not Found')
        else:
            records.sort()
            for each in records:
                print('%07d' % each)


if __name__ == '__main__':
    main()
