1. Знайти боржника по ip "0.1.2.3"

db.debtors.findOne ({
    "ip": "0.1.2.3"
});
 
2. Знайти боржників з м.Дніпро

 db.debtors.find ({
    "city": "Dnipro"
});

3. Боржники із заборгованістю > 100

db.debtors.find ({
    "money": {$gt: 100}
});

4. Боржники із заборгованістю <= 50

db.debtors.find({
    "money": { $lte: 50.50 }
});

5. Боржники із заборгованістю < 500

db.debtors.find({
    "money": { $lt: 500 }
});

6. Знайти боржника по id "66869edb3d99a75afa072f8d"

db.debtors.findOne({
    _id: ObjectId("66869edb3d99a75afa072f8d")
});

7. Видалити з боржників людей, у яких заборгованість <= 50.50

db.debtors.deleteMany(
{ money: { $lte: 50.50 } }
);

8. Знайти боржників з Київа та Харкова

db.debtors.find({
    "city": {
        $in: [
        "Kyiv",
        "Kharkiv"
        ]
    }
});

9. Знайти боржників які не з Дніпра та Харкова

db.debtors.find({
    "city": {
        $nin: [
        "Dnipro",
        "Kharkiv"
        ]
    }
});

10. Знайти боржників, у яких сума заборговагості не 50.50 

db.debtors.find({
    $and: [
    { "money": { $ne: 50.50 } },
    { "money": { $exists: true } }
    ]
});

11. Знайти суму усіх боргів

db.debtors.aggregate([{
   $group: {
       _id: null,
       sum: { $sum: "$money" }
   }
}]);

12. Знайти суму усіх боргів у різній валюті

db.debtors.aggregate([{
   $group: {
       _id: "$currency",
       sum: { $sum: "$money" }
   }
}]);

13. Знайти суму усіх боргів по містам

db.debtors.aggregate([{
   $group: {
       _id: "$city",
       sum: { $sum: "$money" }
   }
}]);


