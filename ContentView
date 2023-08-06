
import SwiftUI

struct ContentView: View {
    
    var body: some View {
        InputView()
        
    }
}

struct InputView: View{
    @State var heightFt: String = ""
    @State var heightIn: String = ""
    @State var weight: String = ""
    @State var age: String = ""
    @State var activityLvl = "Select"
    @State var activityLvlInt: Double = 0.0
    @State var gender: String = "Select"
    @State var goal: String = "Select"
    @State var bmr: Double = 0.0
    @State var tdee: Double = 0.0
    @State var dailyCarbs: Double = 0.0
    @State var dailyProtein: Double = 0.0
    @State var dailyFats: Double = 0.0
    @State var dailyCals: Double = 0.0
    @State var submitHit: Bool = false
    
    var formattedBMR: String {
        return String(format: "%.2f", bmr)
    }

    var formattedTDEE: String {
        return String(format: "%.2f", tdee)
    }

    var formattedDailyCarbs: String {
        return String(format: "%.2f", dailyCarbs)
    }

    var formattedDailyProtein: String {
        return String(format: "%.2f", dailyProtein)
    }

    var formattedDailyFats: String {
        return String(format: "%.2f", dailyFats)
    }

    
    var height: Double? {
        guard let heightFt = Double(heightFt), let heightIn = Double(heightIn) else {
            return nil
        }
        return heightIn + (heightFt * 12)
    }

    
    var weightInt: Double? {
        guard let weight = Double(weight) else{
            return nil
        }
        return weight
    }
    
    
    var ageInt: Double? {
        guard let age = Double(age) else{
            return nil
        }
        return age
    }
    
    func onSubmit(height: Double, weightInt: Double, age: Double, activityLvlInt: Double, gender: String, goal: String) -> (bmr: Double, tdee: Double, dailyCarbs: Double, dailyProtein: Double, dailyFats: Double) {
        submitHit = true
                
        
        let (tdee, bmr, dailyCarbs, dailyProtein, dailyFats) = calcAll(height: height, weightInt: weightInt, age: age, activityLvlInt: activityLvlInt, gender: gender, goal: goal)
        
        

        return (bmr, tdee, dailyCarbs, dailyProtein, dailyFats)
    }

    
    func onClear(){
        submitHit = false
        gender = "Select"
        heightIn = ""
        heightFt = ""
        weight = ""
        age = ""
        activityLvl = "Select"
        goal = "Select"
        
    }
    
    func calcAll(height: Double, weightInt: Double, age: Double, activityLvlInt: Double, gender: String, goal: String) -> (tdee: Double, bmr: Double, dailyCarbs: Double, dailyProtein: Double, dailyFats: Double) {
        let kgWeight: Double = weightInt * 0.4539237
        let cmHeight: Double = height * 2.54
        //var activityLvlInt: Double = 0
                
        
        
        if gender == "Male"{
            let maleCmHeightAge: Double = (4.799 * cmHeight) - (5.677 * age)
            bmr = 88.362 + (13.397 * kgWeight) + maleCmHeightAge
            tdee = bmr * activityLvlInt
            
            // add in second LEFT OF FHRERE
        } else if gender == "Female"{
            bmr = 447.593 + (9.247 * kgWeight) + (3.098 * cmHeight) - (4.330 * age)
            tdee = bmr * activityLvlInt
        }
        
        if goal == "Lose Weight"{
            dailyCals = tdee - 500
            dailyCarbs = (0.4 * dailyCals) / 4
            dailyProtein = (0.3 * dailyCals) / 4
            dailyFats = (0.3 * dailyCals) / 9
            
        } else if goal == "Maintain Weight"{
            dailyCals = tdee
            dailyCarbs = (0.42 * dailyCals) / 4
            dailyProtein = (0.25 * dailyCals) / 4
            dailyFats = (0.3 * dailyCals) / 9
            
        } else if goal == "Gain Weight"{
            dailyCals = tdee + 500
            dailyCarbs = (0.5 * dailyCals) / 4
            dailyProtein = (0.3 * dailyCals) / 9
            dailyFats = (0.2 * dailyCals) / 9
        }
        
        
        
        return (tdee, bmr, dailyCarbs, dailyProtein, dailyFats)
    }
    
    
    
    

    
    var body: some View {
        VStack {
            Text("Macronutrient Calculator").font(.title)
            Spacer()
            HStack{
                Text("Gender").font(.title2)
                    .fontWeight(.regular)
                Spacer()
                Menu {
                    Button {
                        self.gender = "Male"
                    } label: {
                        Text("Male")

                    }
                    Button{
                        self.gender = "Female"
                    } label: {
                        Text("Female")

                    }
                    
                } label: {
                    Text(gender)

                }.font(.title2)
                    .fontWeight(.regular)
                Spacer()
            }
            Group{
                HStack{
                    Text("Height (ft)")
                        .font(.title2)
                        .fontWeight(.regular)
                        .keyboardType(.decimalPad)
                    TextField("", text:$heightFt)
                        .textFieldStyle(.roundedBorder)
                }
                HStack{
                    Text("Height (in)")
                        .font(.title2)
                        .fontWeight(.regular)
                    TextField("", text:$heightIn)
                        .textFieldStyle(.roundedBorder)
                }
                HStack{
                    Text("Weight (lbs)")
                        .font(.title2)
                        .fontWeight(.regular)
                    TextField("", text:$weight)
                        .textFieldStyle(.roundedBorder)
                }
                HStack{
                    Text("Age")
                        .font(.title2)
                        .fontWeight(.regular)
                    TextField("", text:$age)
                        .textFieldStyle(.roundedBorder)
                }
            }
            
            
            Group{
                HStack{
                    Text("Activity level").font(.title2)
                        .fontWeight(.regular)
                    
                    Spacer()
                    Menu {
                        Button {
                            self.activityLvl = "No exercise"
                            self.activityLvlInt = 1.2
                        } label: {
                            Text("Little or no exercise, desk job")
                        }
                        Button{
                            self.activityLvl = "Light exercise"
                            self.activityLvlInt = 1.375
                        } label: {
                            Text("Light exercise or sports 1-3 days a week")
                        }
                        Button{
                            self.activityLvl = "Moderate exercise"
                            self.activityLvlInt = 1.55
                        } label: {
                            Text("Moderate exercise or sports 3-5 days a week")
                        }
                        Button{
                            self.activityLvl = "Hard exercise"
                            self.activityLvlInt = 1.725
                        } label: {
                            Text("Hard exercise or sports 6-7 days a week")
                        }
                        Button{
                            self.activityLvl = "Very hard exercise"
                            self.activityLvlInt = 1.9
                        } label: {
                            Text("Very hard exercise/sports, physical job")
                        }
                        
                    } label: {
                        Text(activityLvl)
                    }.font(.title2)
                        .fontWeight(.regular)
                    Spacer()
                }
            }
            
            
            HStack{
                Text("Goal").font(.title2)
                    .fontWeight(.regular)
                Spacer()
                Menu {
                    Button {
                        self.goal = "Gain Weight"
                    } label: {
                        Text("Gain Weight")
                    }
                    Button{
                        self.goal = "Maintain Weight"
                    } label: {
                        Text("Maintain Weight")
                    }
                    Button{
                        self.goal = "Lose Weight"
                    } label: {
                        Text("Lose Weight")
                    }
                    
                } label: {
                    Text(goal)
                }.font(.title2)
                    .fontWeight(.regular)
                                Spacer()
            }
            .padding(.bottom, 30)
            
            Group{
                HStack{
                    Spacer()
                    Button{
                        
                        guard let height = height, let weightInt = weightInt, let age = ageInt else {
                                            // Handle invalid input if needed.
                                            return
                                        }
                        let (bmr, tdee, dailyCarbs, dailyProtein, dailyFats) = onSubmit(height: height, weightInt: weightInt, age: age, activityLvlInt: activityLvlInt, gender: gender, goal: goal)
                        
                        
                        
                        self.bmr = bmr
                        self.tdee = tdee
                        self.dailyCarbs = dailyCarbs
                        self.dailyProtein = dailyProtein
                        self.dailyFats = dailyFats
                        
                        
                        
                        
                    } label:{
                        Text("Submit").font(.title2)
                            .fontWeight(.regular).padding()
                        
                    }   .background(Color.gray.opacity(0.2))
                        .cornerRadius(10)
                    
                    Spacer()
                    
                    Button{
                        onClear()
                    } label:{
                        Text("Clear").font(.title2)
                            .fontWeight(.regular).padding()
                        
                    }   .background(Color.gray.opacity(0.2))
                        .cornerRadius(10)
                    Spacer()
                }
                Spacer()
                if submitHit{
                    Group{
                        Text("BMR \(formattedBMR)").padding()
                        Text("TDEE \(formattedTDEE)").padding()
                        Text("Daily Carbs \(formattedDailyCarbs)").padding()
                        Text("Daily Protein \(formattedDailyProtein)").padding()
                        Text("Daily Fats \(formattedDailyFats)").padding()
                    }
                }
            }
            
            
            
            Spacer()

        }.padding()
    }
}





struct ContentView_Previews: PreviewProvider {
    static var previews: some View {
        ContentView()
    }
}

struct ContentView2_Previews: PreviewProvider {
    static var previews: some View {
        ContentView().preferredColorScheme(.dark)
    }
}
