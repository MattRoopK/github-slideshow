def main(player):
    # example: [["David", [inventory], [weapon scores]]
    #Turn Start!
    print(player[0] + "'s turn!")
    #Roll Terrain Dice (1, 2, 2, 3, 4, 4)x2
    print("Rolling the terrain dice:")
    t1 = random.choice([1, 2, 2, 3, 4, 4])
    t2 = random.choice([1, 2, 2, 3, 4, 4])
    print("You rolled:", t1, "and", t2)
    #Determine provision count needed
    p_needed = t1+t2
    print("You need", p_needed, "provisions.")
    #Roll Weapon Dice (Axe-1, Axe-2, Bow-1, Bow-2, Sword-1, Sword-2)x2
    w_axe = 0
    w_bow = 0
    w_sword = 0
    for i in range(2):
        w = random.randrange(1, 7)
        if w == 1:
            print("   Axe 1")
            w_axe += 1
        elif w == 2:
            print("   Axe 2")
            w_axe += 2
        elif w == 3:
            print("   Bow 1")
            w_bow += 1
        elif w == 4:
            print("   Bow 2")
            w_bow += 2
        elif w == 5:
            print("   Sword 1")
            w_sword += 1
        else:
            print("   Sword 2")
            w_sword += 2
    print("Your weapon skills are:")
    if w_axe > 0: print("Axe:", w_axe)
    if w_bow > 0: print("Bow:", w_bow)
    if w_sword > 0: print("Sword:", w_sword)
    #Associate weapon stats with player
    if len(player) == 2:
        player.append([w_axe, w_bow, w_sword])
    else:
        player[2] = [w_axe, w_bow, w_sword]
    #Any passed magic rerolls?
    if "reroll" in player[1]:
        has_a_reroll = True
        while has_a_reroll:
            rr_count = player[1].count("reroll")
            if rr_count > 1:
                print("** You have", rr_count, "magic rerolls! **")
                text = "one"
            else:
                print("** You have a magic reroll! **")
                text = "it"
            #Use them?
            print("Do you want spend", text, "to reroll a terrain die? (y/n)")
            user = get_valid_entry(["Y", "y", "N", "n"])
            if user.lower() == "y":
                print("Reroll which die: a-"+str(t1), "b-"+str(t2), "(a/b)")
                d = get_valid_entry(["A", "a", "B", "b"])
                if d.lower() == "a":
                    t1 = random.choice([1, 2, 2, 3, 4, 4])
                    print("Dice A is now:", t1)
                else:
                    t2 = random.choice([1, 2, 2, 3, 4, 4])
                    print("Dice B is now:", t2)
                print(t1, t2)
                p_needed = t1+t2
                print("You now need", p_needed, "provisions.")
                #remove reroll from inventory
                player[1].remove("reroll")
                #player has a 2nd reroll?
                if "reroll" not in player[1]:
                    has_a_reroll = False
            else:
                has_a_reroll = False
    #Any passed portcullis?
    if "portcullis" in player[1]:
        print("** You have a portcullis! **")
        print("You may by pass a terrain die!")
        #   Use on which number?
        print("Which die to bypass: a-"+str(t1), "b-"+str(t2), "(a/b)")
        d = get_valid_entry(["A", "a", "B", "b"])
        if d.lower() == "a":
            print("You bypass the terrain!")
            p_needed -= t1
        else:
            print("You bypass the terrain!")
            p_needed -= t2
        print("You now only need", p_needed, "provisions.")
        #remove portcullis from inventory
        player[1].remove("portcullis")
    #Any saved provisions?
    if "food" in player[1]:
        total_food = player[1].count("food")
        print("You have", total_food, "provisions saved from earlier.")
        #   Adjust provision count
        p_needed -= total_food
        #Have enough?
        if p_needed > 0:
            if p_needed == 1:
                print("You still need to get 1 provision.")
            else:
                print("You still need to get", p_needed, "provisions.")
        else:
            if p_needed < 0:
                print("You have more than you need!")
                print("Unfortunately, you cannot keep old provisions,")
                print("   as the food will expire...")
            else:
                print("You don't need any provisions!")
            p_needed = 0
        #remove all saved food in inventory
        while "food" in player[1]:
            player[1].remove("food")
    #ENSURE USED ITEMS ARE DELETED PROPERLY before continuing
    print(player)
    #Proceed to resource gathering phase
    gather_resources(player)
