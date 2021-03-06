![Agency Logo](https://repository-images.githubusercontent.com/381489249/37b6c900-da8a-11eb-90cb-6e291ea3974c)

<a href='https://ko-fi.com/X8X356QT4' target='_blank'><img height='36' style='border:0px;height:36px;' src='https://cdn.ko-fi.com/cdn/kofi2.png?v=2' border='0' alt='Buy Me a Coffee at ko-fi.com' /></a>

# Agency
This is a PoC framework for autonomous, plan-making agents.

<br />

## About
Agency provides a .NET 5 framework for autonomous agents (referred to as actors in agency) who can form their own plans. 
They are able to do this by chaining a number of actions together until they are able to execute their plan.

Each action contains a set of inputs and a set of outputs. These sets are made up of assets that are required for the action (inputs), or that are gained by doing the action (outputs). 
Actors try to form plans by looking at a goal they have and seeing what inputs are required. 
The actor will then look through all available actions to find one that provides at least one of those inputs as an output. This action is then appended to the plan, and the search continues.
Actions previously selected have their inputs added to search until the actor's available assets are able to meet those inputs.

<br />

## Installation
To install the Agency library and use it in your project, you can either use the NuGet package manager:

```
dotnet add PROJECT package Agency
```

or download the source code from the GitHub repository:

```
https://github.com/Manny-coffee-dev/Agency.git
```

<br />

## Usage
### Basic Usage
To make use of the Agency framework, where an Actor's goals are defined by the user, a number of steps need to be completed:

1) Import the library
```
using Agency;

namespace Main
{
    class Program
    {

    }
}
```

2) Create an Actor
```
using Agency;

namespace Main
{
    class Program
    {
        Actor agent = new();
    }
}

```

3) Create Assets
```
using Agency;

namespace Main
{
    ...

    class MyAsset : Asset
    {
        public float Value { get; set; }

        public MyAsset(float value)
        {
            this.Value = value;
        }
    }
}
```

4) Create Actions
```
using Agency;

namespace Main
{
    ...

    class MyAction : Action
    {
        public MyAction()
        {
            InputAssets = new List<Asset>();
            OutputAssets = new List<Asset>();
            InputTraits = new List<Trait>();
            OutputTraits = new List<Trait>();
        }
    }
}
```

5) Assign Assets/Actions to the Actor
```
using Agency;

namespace Main
{
    class Program
    {
        Actor agent = new();

        agent.AvailableAssets.Add(new MyAsset(100));
        MyAction action = new MyAction();
        action.OutputAssets.Add(new MyAsset(100));
        agent.AvailableActions.Add(action);
        agent.Goals.Add(new MyAction());
    }

    ...
}
```

6) Let the Actor create a plan
```
{
    class Program
    {
        Actor agent = new();
        agent.AvailableAssets.Add(new MyAsset(100));
        agent.Goals.Add(new MyAction());
        agent.Think();
    }

    ...
}
```

### Advanced Usage
To make use of the Agency framework, where an Actor defines their own goals using needs, a number of steps need to be completed:

1) Import the library
```
using Agency;

namespace Main
{
    class Program
    {

    }
}
```

2) Create an Actor
```
using Agency;

namespace Main
{
    class Program
    {
        Actor agent = new();
    }
}

```

3) Create Assets
```
using Agency;

namespace Main
{
    ...

    class MyAsset : Asset
    {
        public float Value { get; set; }

        public MyAsset(float value)
        {
            this.Value = value;
        }
    }
}
```

4) Create Needs
```
using Agency;

namespace Main
{
    ...

    class MyNeed : Need
    {

        public MyNeed(double level) : base(level)
        {
            Level = level;
            PositiveTraits = new List<Trait>();
            NegativeTraits = new List<Trait>();
        }
    }
}
```

5) Create Actions
```
using Agency;

namespace Main
{
    ...

    class MyAction : Action
    {
        public MyAction()
        {
            Inputs = new List<Asset>();
            Outputs = new List<Asset>();
        }
    }
}
```

7) Create Traits
```
using Agency;

namespace Main
{
    ...

    class MyTrait : Trait
    {
        public MyTrait()
        {
        }
    }
}

8) Assign traits to Action/Need and Action/Need to the Actor
```
using Agency;

namespace Main
{
    class Program
    {
        Actor agent = new();

        MyNeed need = new MyNeed(1.0);
        need.PositiveTraits.Add(new MyTrait());

        MyAction action = new MyAction();
        action.OutputAssets.Add(new MyAsset(100));
        action.OutputTraits.Add(new MyTrait());

        agent.Needs.Add(need);
        agent.AvailableActions.Add(action);
    }

    ...
}
```

9) Assign Assets to the Actor and let the Actor define their goal
```
using Agency;

namespace Main
{
    class Program
    {
        Actor agent = new();

        MyNeed need = new MyNeed(1.0);
        need.PositiveTraits.Add(new MyTrait());

        MyAction action = new MyAction();
        action.OutputAssets.Add(new MyAsset(100));
        action.OutputTraits.Add(new MyTrait());

        agent.Needs.Add(need);
        agent.AvailableActions.Add(action);

        agent.SelectGoals();
    }

    ...
}
```

10) Let the Actor create a plan
```
{
    class Program
    {
        Actor agent = new();

        MyNeed need = new MyNeed(1.0);
        need.PositiveTraits.Add(new MyTrait());

        MyAction action = new MyAction();
        action.OutputAssets.Add(new MyAsset(100));
        action.OutputTraits.Add(new MyTrait());

        agent.Needs.Add(need);
        agent.AvailableActions.Add(action);

        agent.SelectGoals();
        agent.Think();
    }

    ...
}
```


### Examples
An example of usage of the Agency framework can be found in the Example directory of this codebase.

<br />

## Road Map
This section details planned releases for the Agency framework. Agency uses [Semantic Versioning 2.0.0](https://semver.org/) for tracking codebase versions. Until the framework stablises, 
Agency will use 0.X.Y versions during the alpha phase of development. Once the PoC is complete, a stable 1.0.0 release will be created.

### Initial Pre-Alpha Release - [Rational Agent](https://github.com/Manny-coffee-dev/Agency/milestone/1) - v0.1.0 - Completed
An intial release containing a basic framework to allow the development of agents which can form and execute rational plans based on their internal goals.

### Update 1 - [Behavioural Agent](https://github.com/Manny-coffee-dev/Agency/milestone/3) - v0.2.0 - Completed
This update brings traits which allow recording of data about an agent or asset. These traits also allow for the change of an agent/asset's behaviour.

### Update 2 - [Needy Agent](https://github.com/Manny-coffee-dev/Agency/milestone/2) - v0.3.0 - Completed
An expanded modelling of an agent's internal state. This update adds needs that drive internal goal selection in response to changes in an agent's state.


## Support This Project
You can support this project by using it and raising any issues using our [Issues tracker](https://github.com/Manny-coffee-dev/Agency/issues) or contribute directly
by raising pull requests with bug fixes and new features.

You can also support us by buying some merchandise from our eco-sustainable partners at [TeeMill](https://coffeebreakdev.teemill.com/).
We receive a proportion of the cost of each item you purchase. If merchandise isn't your thing, consider [buying us a coffee](https://ko-fi.com/coffeebreakdevs) to support our work!
This update brings traits which allow recording of data about an agent or asset. These traits also allow for the change of an agent/asset's behaviour.
