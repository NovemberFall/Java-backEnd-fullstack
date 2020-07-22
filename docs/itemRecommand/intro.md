# Item Recommendation

- 为什么要设计这个 Project? 已经有了 Yelp API 为什么要设计这个？
  - 因为 Yelp 是给本地人服务的，并不是为你个性服务，比如 中餐馆 是美式中餐，比如 panda express
  - personalization:
    - 假设你到达目的地要2小时，你现在已经很饿了，并且是 11:45 AM
      - 所以可以利用 Google Map API
    - 假如你已经到达一个餐馆，但是很多人排队 
      - Yelp 如何解决？ 但是 Yelp 没有做，所以我们可以做
    - 分析用户的 comment, 比如餐馆服务不好，但是 yelp 没有做
      - 价格 so expensive, 或者菜单已经变了， 比如 cash only   
      - 你如你觉得不好吃，you just give 5 % tip, 服务员冲出来要 18% tip
      - 所以假如这种情况： 你去过一次再也不想去了
    - Amazon 是否解决你所有买买买的需求？
      - 比如：你买了一个铸铁锅，然后他一直给你买铸铁锅   
      - 然后比如总是图片比实物好
    - Facebook, 反复提醒要不要加这个人，反复提醒 
    - Google Ads: 两颗红豆的例子, 不小心点了，它就一直推送这个广告
    - Youtube Ads 系统里的广告，
      - 放在前5秒，那么你可以了解用户是否喜欢自己的广告，之后你会根据此来改进 

