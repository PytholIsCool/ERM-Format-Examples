# ERM-Format-Examples

This is the file format I use for rename maps to anybody who's interested.

``` erm
erm {
  game="Demo"
}

asm name="Assembly-CSharp" {

# rename a specific type
typ name="OldType", namespace="Demo.Namespace" {
  name="NewType"
  namespace="Demo.Renamed"
}

# match using full type selectors
typ name="TargetType", namespace="Demo", base="UnityEngine.MonoBehaviour", flds=3, mtds=5, ifaces=1, gargs=0, acc=public, abstract=false, sealed=false, kind=class {
  name="FullyMatchedType"
}

# require a field and method to exist
typ {
  mem {
    fld name="health"
    mtd name="TakeDamage"
  }
  name="HasHealthAndDamage"
}

# require method and exclude another
typ {
  mem {
    mtd name="Update"
    !mtd name="FixedUpdate"
  }
  name="UpdateOnlyType"
}

# match field properties
typ {
  mem {
    fld name="speed", acc=private, static=false
  }
  name="HasPrivateSpeedField"
}

# match method properties
typ {
  mem {
    mtd name="Move", params=2, acc=public, static=false
  }
  name="MoveMethodType"
}

# match first parameter type
typ {
  mem {
    mtd name="Init" {
      prm[0] {
        typ name="System.String"
      }
    }
  }
  name="InitWithString"
}

# match parameter names
typ {
  mem {
    mtd name="Configure", param_names=["x","y","z"]
  }
  name="ConfigureXYZ"
}

# check first field name
typ {
  mem {
    fld[0] name="firstField"
  }
  name="FirstFieldMatch"
}

# check first method name
typ {
  mem {
    mtd[0] name="Awake"
  }
  name="FirstMethodAwake"
}

# check field type
typ {
  mem {
    fld name="controller" {
      typ name="PlayerController"
    }
  }
  name="HasControllerField"
}

# check method return type
typ {
  mem {
    mtd name="GetPlayer" {
      typ name="Player"
    }
  }
  name="ReturnsPlayer"
}

# rename type of first field
typ {
  mem {
    fld name="weapon"
  }

  fld[0] {
    typ {
      name="Weapon"
      namespace="Game.Items"
    }
  }

  name="WeaponHolder"
}

# resolve nested type path (e.g. list element)
typ {
  mem {
    fld name="list" {
      typ[0] {
        name="ElementType"
      }
    }
  }
  name="ListHolder"
}

# match by base type
typ base="BaseClass" {
  name="DerivedRenamed"
}

# match interfaces, structs, enums
typ kind=interface {
  name="RenamedInterface"
}

typ kind=struct {
  name="RenamedStruct"
}

typ kind=enum {
  name="RenamedEnum"
}

# match access level
typ acc=private {
  name="PrivateTypeRenamed"
}

# match static field
typ {
  mem {
    fld name="Instance", static=true
  }
  name="SingletonType"
}

# deep nested traversal
typ {
  mem {
    fld name="player" {
      typ {
        fld name="inventory" {
          typ {
            name="Inventory"
          }
        }
      }
    }
  }
  name="PlayerWithInventory"
}

# require one field and exclude another
typ {
  mem {
    fld name="enabled"
    !fld name="disabled"
  }
  name="EnabledOnly"
}

# apply multiple child actions
typ {
  mem {
    mtd name="Start"
  }

  fld[0] {
    name="renamedField"
  }

  mtd[0] {
    name="RenamedMethod"
  }

  name="MultiModifiedType"
}

}
```
