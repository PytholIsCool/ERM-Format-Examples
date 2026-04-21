# ERM-Format-Examples

This is the file format I use for rename maps to anybody who's interested.

``` erm
erm {
  game="TestGame",
  build="1.0.0"
} erm
# 'game' required, 'build' optional

asm name="Assembly-CSharp" {

    typ name="Player",namespace="Game.Core",flds=5,mtds=12,ifaces=2,gargs=1,acc=public,abstract=false,sealed=false,kind=class {
        # Any new names are defined inside the typ block
        name="PlayerRenamed"
        namespace="Game.Core.Renamed"

        # You can use members inside a class to profile classes as well.
        # This is particularly useful for any obfuscated classes that have members with names that stay unobfuscated
        mem {
            mtd name="Move",ret="System.Void",params=2,gargs=0,acc=public,static=false
            fld name="health",type="System.Int32",acc=private,static=false
        } mem

        mtd name="Jump" {
            name="DoJump"
        } mtd
        mtd name="Move",params=2 {
            name="MoveExact"
        } mtd
        mtd ret="System.Void",params=0 {
            name="VoidMethod"
        } mtd
        mtd name="GenericMethod",gargs=1 {
            name="GenericRenamed"
        } mtd
        mtd acc=protected_internal {
            name="ProtectedInternalMethod"
        } mtd
        mtd static=true {
            name="StaticMethodRenamed"
        } mtd

        fld name="health" {
            name="hp"
        } fld
        fld type="System.Int32" {
            name="intField"
        } fld
        fld acc=private_protected {
            name="ppField"
        } fld
        fld static=true {
            name="staticField"
        } fld
    } typ

    typ name="GameState",kind=enum,acc=public {
        name="GameStateRenamed"
    } typ

    typ name="Vector3",kind=struct,sealed=true {
        name="Vec3"
    } typ

    typ name="IMovable",kind=interface,abstract=true {
        name="IMovableRenamed"
    } typ

    typ acc=internal,flds=0,mtds=0 {
        name="EmptyInternalType"
    } typ
} asm
```
